###bash 特殊字符 

    [原网页地址](http://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/x361.html)

```
- Position the Cursor:
  \033[<L>;<C>H
     Or
  \033[<L>;<C>f
  puts the cursor at line L and column C.
- Move the cursor up N lines:
  \033[<N>A
- Move the cursor down N lines:
  \033[<N>B
- Move the cursor forward N columns:
  \033[<N>C
- Move the cursor backward N columns:
  \033[<N>D

- Clear the screen, move to (0,0):
  \033[2J
- Erase to end of line:
  \033[K

- Save cursor position:
  \033[s
- Restore cursor position:
  \033[u
```
这里的东西没仔细看，先复制过来

> The latter two codes are NOT honoured by many terminal emulators.
> The only ones that I'm aware of that do are xterm and nxterm - even though the majority of terminal emulators are based on 
> xterm code. As far as I can tell, rxvt, kvt, xiterm, and Eterm do not support them. They are supported on the console.

这里有个demo，举个栗子：

```
[root@localhost]# printf '#!/bin/bash\necho doing something evil!\nexit\n\033[2Aechodoing something very nice!\n' > backdoor.sh
[root@localhost]# cat backdoor.sh 
#!/bin/bash
echodoing something very nice!
[root@localhost]# chmod +x backdoor.sh 
[root@localhost]# ./backdoor.sh 
doing something evil!
[root@localhost]# 
```

