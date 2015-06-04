#代码
`time echo "scale=5000; 4*a(1)" | bc -l -q`

tar cvpzf gentoo.tgz --exclude=/proc --exclude=/sys --exclude=/dev --exclude=/lost+found --exclude=/run --exclude=/tmp --exclude=/test /

**************************************************************
KiwiVM Task File, executed: Wed, 22 Apr 2015 02:24:19 -0400
**************************************************************
OS: CentOS 6 i686
Loaded plugins: fastestmirror
Setting up Install Process
Loading mirror speeds from cached hostfile
 * base: centos.arvixe.com
 * epel: linux.mirrors.es.net
 * extras: mirrors.psychz.net
 * updates: mirror.pac-12.org
Resolving Dependencies
--> Running transaction check
---> Package python-setuptools.noarch 0:0.6.10-3.el6 will be installed
nished Dependency Resolution

Dependencies Resolved

================================================================================
 Package                  Arch          Version               Repository   Size
================================================================================
Installing:
 python-setuptools        noarch        0.6.10-3.el6          base        336 k

Transaction Summary
================================================================================
Install       1 Package(s)

Total download size: 336 k
Installed size: 1.5 M
Downloading Packages:
Running rpm_check_debug
Running Transaction Test
Transaction Test Succeeded
Running Transaction

  Installing : python-setuptools-0.6.10-3.el6.noarch                        1/1 

  Verifying  : python-setuptools-0.6.10-3.el6.noarch                        1/1 

Installed:
  python-setuptools.noarch 0:0.6.10-3.el6                                       

Complete!
Searching for pip
Reading http://pypi.python.org/simple/pip/
Best match: pip 6.1.1
Downloading https://pypi.python.org/packages/source/p/pip/pip-6.1.1.tar.gz#md5=6b19e0a934d982a5a4b798e957cb6d45
Processing pip-6.1.1.tar.gz
Running pip-6.1.1/setup.py -q bdist_egg --dist-dir /tmp/easy_install-tWogNh/pip-6.1.1/egg-dist-tmp-AfgfHZ
warning: no previously-included files found matching '.coveragerc'
warning: no previously-included files found matching '.mailmap'
warning: no previously-included files found matching '.travis.yml'
warning: no previously-included files found matching 'pip/_vendor/Makefile'
warning: no previously-included files found matching 'tox.ini'
warning: no previously-included files found matching 'dev-requirements.txt'
no previously-included directories found matching '.travis'
no previously-included directories found matching 'docs/_build'
no previously-included directories found matching 'contrib'
no previously-included directories found matching 'tasks'
no previously-included directories found matching 'tests'
Adding pip 6.1.1 to easy-install.pth file
Installing pip script to /usr/bin
Installing pip2.6 script to /usr/bin
Installing pip2 script to /usr/bin

Installed /usr/lib/python2.6/site-packages/pip-6.1.1-py2.6.egg
Processing dependencies for pip
Finished processing dependencies for pip
/usr/lib/python2.6/site-packages/pip-6.1.1-py2.6.egg/pip/_vendor/requests/packages/urllib3/util/ssl_.py:79: InsecurePlatformWarning: A true SSLContext object is not available. This prevents urllib3 from configuring SSL appropriately and may cause certain SSL connections to fail. For more information, see https://urllib3.readthedocs.org/en/latest/security.html#insecureplatformwarning.
  InsecurePlatformWarning
Collecting shadowsocks
/usr/lib/python2.6/site-packages/pip-6.1.1-py2.6.egg/pip/_vendor/requests/packages/urllib3/util/ssl_.py:79: InsecurePlatformWarning: A true SSLContext object is not available. This prevents urllib3 from configuring SSL appropriately and may cause certain SSL connections to fail. For more information, see https://urllib3.readthedocs.org/en/latest/security.html#insecureplatformwarning.
  InsecurePlatformWarning
  Downloading shadowsocks-2.6.8.tar.gz
Installing collected packages: shadowsocks
  Running setup.py install for shadowsocks
Successfully installed shadowsocks-2.6.8
2015-04-22 02:24:27 INFO     loading libcrypto from libcrypto.so.10

******************************************************************
* Completed.                                                     *
******************************************************************
*** End of transmission ***
