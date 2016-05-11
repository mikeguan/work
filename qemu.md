1.为了支持多构架,在make.conf中设置QEMU支持的虚拟机类型.其它的构架还没有尝试过,不过至少支持x86和x86_64两种构架
QEMU_SOFTMMU_TARGETS="x86_64 i386 arm mips mips64 mips64el mipsel"

2.创建磁盘文件.
磁盘镜像格式有raw,cow,qcow,qcow2,vmdk,vdi等格式,读者可以自行比较.总体来说，qcow2支持COW，快照，磁盘压缩，使用起来性能不错,而且可以转换成raw格式，所以推荐之.
➜  Machines  qemu-img create -f qcow2 gentoo.img 40G
Formatting 'gentoo.img', fmt=qcow2 size=42949672960 encryption=off cluster_size=65536 lazy_refcounts=off 

3.编写启动文件
➜  ~  cat bin/start_gentoo.sh 
#!/bin/sh
exec qemu-system-i386 -enable-kvm \
        -cpu host \
        -drive file=/home/this/should/be/safe/Machines/gentoo.img,if=virtio \
        -net nic -net user,hostname=gentoovm \
        -m 1000M \
        -name "Gentoo ~i386 VM" \
        $@
➜  ~  
qemu支持的选项很多很专业,这里先这么用.注意,如果用图形界面的Linux作为Host机器,就像上面,然后启动命令为
➜  ~  bin/start_gentoo.sh -boot d -cdrom bin/install-x86-minimal-20141209.iso  -redir tcp:50022::22 
在Guest机器上,就可以使用
net-setup enp0s3来dhcp配置网络,设置root密码,然后启动sshd服务进行配置.那么,接下来就可以在Host机器上ssh连接了

4.上面的-net user是走NAT的，所以VM对于外网是不可以见的。如果需要Guest对外部可见,就需要使用桥接，根据手册有一个简单的配置方法:
对于HOST主机，由于使用了systemd，所以配置自动桥接如下：
➜  locale  ls /etc/systemd/network
br0.netdev  br0.network  enp1s0.network
➜  locale  cat /etc/systemd/network/br0.netdev
[NetDev]
Name=br0
Kind=bridge
➜  locale  cat /etc/systemd/network/br0.network
[Match]
Name=br0
[Network]
DNS=172.31.1.1
Address=192.168.0.5/24
Gateway=192.168.0.189
➜  locale  cat /etc/systemd/network/enp1s0.network
[Match]
Name=enp1s0
[Network]
Bridge=br0
➜  locale
➜  locale  sudo systemctl enable systemd-networkd  
➜  locale  sudo systemctl restart systemd-networkd  

这样，系统启动的时候，就会产生一个br0的桥设备。
然后打开qemu的桥支持：
➜  locale  cat /etc/qemu/bridge.conf
# This should have the following permissions: root:qemu 0640
 allow br0
然后，启动虚拟机的时候，使用-net bridge,br=br0来就可以了。
最终，部署启动使用的启动脚本为
➜  locale  cat /home/user/bin/start_debian_remote.sh
#!/bin/sh
exec qemu-system-i386 -enable-kvm \
     -cpu host -smp 2,sockets=1 \
     -drive file=/home/user/VirtualMachine/Machines/debian_7.img,if=virtio \
     -net nic,model=virtio -net bridge,br=br0 \
     -m 2048M \
     -name "Debian Wheezy VM" \
     -monitor stdio \
     -vnc :0
     $@
➜  locale
注意，如果发现不能引导等原因，可能是virtio没有设置正确。记得
➜  Machines2  sysystemctl enable libvirtd.service
➜  Machines2  sysystemctl restart libvirtd.service

5.虚拟机的管理(主要是对qemu进行磁盘的备份和恢复操作)
➜  Machines2  qemu-img info gentoo.img
image: gentoo.img
file format: qcow2
virtual size: 35G (37580963840 bytes)
disk size: 4.0G
cluster_size: 65536
Format specific information:
    compat: 1.1
    lazy refcounts: false
➜  Machines2  qemu-img snapshot -c orig gentoo.img
➜  Machines2  qemu-img snapshot -l gentoo.img
Snapshot list:
ID        TAG                 VM SIZE                DATE       VM CLOCK
1         orig                      0 2015-03-06 01:44:49   00:00:00.000
➜  Machines2
--操作虚拟机,读写磁盘--
➜  Machines2  qemu-img snapshot -c snaptest gentoo.img
➜  Machines2  qemu-img snapshot -l gentoo.img
Snapshot list:
ID        TAG                 VM SIZE                DATE       VM CLOCK
1         orig                      0 2015-03-06 01:44:49   00:00:00.000
2         snaptest                  0 2015-03-06 02:05:58   00:00:00.000
➜  Machines2
然后就可以随便的切换磁盘快照了
➜  Machines2  qemu-img snapshot -a orig gentoo.img
➜  Machines2  qemu-img snapshot -a snaptest gentoo.img
以及删除无用的磁盘快照
➜  Machines2  qemu-img snapshot -d orig gentoo.img
➜  Machines2  qeqemu-img snapshot -l gentoo.img
Snapshot list:
ID        TAG                 VM SIZE                DATE       VM CLOCK
2         snaptest                  0 2015-03-06 02:05:58   00:00:00.000
➜  Machines2

6.调试内核
调试内核的时候,上面的脚本是不能使用的,可能是sh脚本对于$@参数传递有问题.那么就可以直接的命令行来写全,制定需要的内核+ramdisk+额外的启动参数:
➜  ~  qemu-system-x86_64 -enable-kvm -cpu host -smp 2,sockets=1 -drive file=/home/user/VirtualMachine/Machines2/gentoo.img,if=virtio,cache=writethrough -net nic,model=virtio,macaddr=52:54:21:63:73:45 -net bridge,br=br0 -m 1024M -name "Gentoo VM" -monitor stdio -vnc :1 -kernel /boot/kernel-genkernel-x86_64-3.18.7-gentoo -initrd /boot/initramfs-genkernel-x86_64-3.18.7-gentoo -append "root=/dev/vda3 init=/usr/lib/systemd/systemd" -serial telnet:127.0.0.1:4444,server

然后再host主机可以控制串口
➜  ~  telnet 127.0.0.1 4444
Trying 127.0.0.1...
Connected to 127.0.0.1.
Escape character is '^]'.
Initializing cgroup subsys cpuset
Initializing cgroup subsys cpuacct
Linux version 3.18.7-gentoo (root@localhost) (gcc version 4.8.3 (Gentoo 4.8.3 p1.1, pie-0.5.9) ) #2 SMP Wed Mar 11 12:32:31 2015

如果需要更多的启动信息，可以修改内核的启动参数
-append "root=/dev/vda3 init=/usr/lib/systemd/systemd console=uart8250,io,0x3f8 debug ignore_loglevel"
启动得到的消息如下所示:
➜  ~  telnet 127.0.0.1 4444
Trying 127.0.0.1...
Connected to 127.0.0.1.
Escape character is '^]'.
early console in setup code
early console in decompress_kernel
Decompressing Linux... Parsing ELF... done.

7.对于使用genkernel工具来产生kernel和initramfs,是需要root权限的.为了不和Host主机的环境有干扰和破坏,可以制定genkernel的参数,用一般用户来生成结果
修改/usr/share/genkernel/gen_initramfs.sh文件,有如下两条命令是需要用sudo来执行的
➜  linux git:(master) cat /usr/share/genkernel/gen_initramfs.sh | grep sudo
    sudo mknod -m 660 console c 5 1 || gen_die "cannot mknod"
    sudo mknod -m 660 null c 1 3 || gen_die "cannot mknod"
    sudo mknod -m 660 zero c 1 5 || gen_die "cannot mknod"
    sudo mknod -m 600 tty0 c 4 0 || gen_die "cannot mknod"
    sudo mknod -m 600 tty1 c 4 1 || gen_die "cannot mknod"
    sudo mknod -m 600 ttyS0 c 4 64 || gen_die "cannot mknod"
    sudo cpio --quiet -i -F "${CPIO}" 2> /dev/null \
    sudo rm -r "${TDIR}"
➜  linux git:(master) 
编译内核的命令使用
➜  linux git:(master) genkernel all --kerneldir=/home/user/Study/GitHub/linux --bootdir=/home/user/VirtualMachines/Machines/tmp_boot --logfile=/home/user/VirtualMachines/Machines/genkernel.log  --module-prefix=/home/user/VirtualMachines/Machines/tmp_boot --no-clean


更新: skip with genkernel
genkernel不太喜欢用，毕竟是gentoo专有的东西，这里介绍推荐使用dracut
# required by dracut (argument)
=sys-kernel/dracut-043-r2 ~amd64
emerge -auDN dracut
（其它发行版默认应该都装了的）

➜  ~ cd Study/GitHub/linux
➜  linux git:(master) mkdir ../INSTALL_PATH
#配置内核
➜  linux git:(master) make
➜  linux git:(master) make INSTALL_PATH=../INSTALL_PATH install
sh ./arch/x86/boot/install.sh 4.2.0-rc7+ arch/x86/boot/bzImage \
        System.map "../INSTALL_PATH"
➜  linux git:(master) make INSTALL_MOD_PATH=../INSTALL_PATH modules_install
➜  linux git:(master) cd ../INSTALL_PATH
➜  INSTALL_PATH ls
config-4.2.0-rc7+      lib                        vmlinuz-4.2.0-rc7+
config-4.2.0-rc7+.old  System.map-4.2.0-rc7+      vmlinuz-4.2.0-rc7+.old
initramfs.img          System.map-4.2.0-rc7+.old
➜  INSTALL_PATH sudo dracut -f -v -k './lib/modules/4.2.0-rc7+' initramfs.img 4.2.0-rc7+

运行
➜  INSTALL_PATH qemu-system-x86_64 -enable-kvm -cpu host -smp 2,sockets=1 -drive file=Fedora.img,if=virtio,cache=writethrough   -serial telnet:127.0.0.1:4444,server -kernel ~/Study/GitHub/INSTALL_PATH/vmlinuz-4.2.0-rc7+ -initrd ~/Study/GitHub/INSTALL_PATH/initramfs.img -append "root=/dev/vda1 init=/usr/lib/systemd/systemd console=uart8250,io,0x3f8 debug ignore_loglevel"

➜  INSTALL_PATH telnet 127.0.0.1 4444
