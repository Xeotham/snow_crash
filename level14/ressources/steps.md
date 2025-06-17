When we started the **level14** there is nothing.
We where a bit clueless, we started re reading previous levels to find any clue, but nothing.
But we had an idea, there is one thing we hadn't check: The getflag executable !

We used string on it:
```bash
level13@SnowCrash:~$ strings /bin/getflag
```

With this we saw it used getuid, like in the **level13**, to check if the user is correct, and ptrace.

After some research, [in this article](https://bases-hacking.org/ptrace.html), it explain that ptrace is used for debugging, and it return 0 if all is good, and -1 if a ptrace is already running.

When using gdb for the first time, we tried to get to getuid but it exited before it. We thought it was cause by ptrace.

So we got to ptrace and changed it's return value to 0.

```bash
(gdb) disas
Dump of assembler code for function main:
   0x08048946 <+0>:	push   %ebp
   0x08048947 <+1>:	mov    %esp,%ebp
   0x08048949 <+3>:	push   %ebx
   0x0804894a <+4>:	and    $0xfffffff0,%esp
   0x0804894d <+7>:	sub    $0x120,%esp
   0x08048953 <+13>:	mov    %gs:0x14,%eax
   0x08048959 <+19>:	mov    %eax,0x11c(%esp)
   0x08048960 <+26>:	xor    %eax,%eax
   0x08048962 <+28>:	movl   $0x0,0x10(%esp)
   0x0804896a <+36>:	movl   $0x0,0xc(%esp)
   0x08048972 <+44>:	movl   $0x1,0x8(%esp)
   0x0804897a <+52>:	movl   $0x0,0x4(%esp)
   0x08048982 <+60>:	movl   $0x0,(%esp)
   0x08048989 <+67>:	call   0x8048540 <ptrace@plt>
=> 0x0804898e <+72>:	test   %eax,%eax
   0x08048990 <+74>:	jns    0x80489a8 <main+98>
   0x08048992 <+76>:	movl   $0x8048fa8,(%esp)
   0x08048999 <+83>:	call   0x80484e0 <puts@plt>
   0x0804899e <+88>:	mov    $0x1,%eax
   0x080489a3 <+93>:	jmp    0x8048eb2 <main+1388>
   0x080489a8 <+98>:	movl   $0x8048fc4,(%esp)
   0x080489af <+105>:	call   0x80484d0 <getenv@plt>
   0x080489b4 <+110>:	test   %eax,%eax
   0x080489b6 <+112>:	je     0x80489ea <main+164>
   0x080489b8 <+114>:	mov    0x804b040,%eax
   0x080489bd <+119>:	mov    %eax,%edx
   0x080489bf <+121>:	mov    $0x8048fd0,%eax
   0x080489c4 <+126>:	mov    %edx,0xc(%esp)
   0x080489c8 <+130>:	movl   $0x25,0x8(%esp)
   0x080489d0 <+138>:	movl   $0x1,0x4(%esp)
   0x080489d8 <+146>:	mov    %eax,(%esp)
   0x080489db <+149>:	call   0x80484c0 <fwrite@plt>
   0x080489e0 <+154>:	mov    $0x1,%eax
   [...]
(gdb) set $eax = 0
```
It worked !! We got through the verification !!

We then goes to getuid and change it's return value to 3014, which is flag14's UID.

```bash
level14@SnowCrash:~$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
[...]
level14:x:2014:2014::/home/user/level14:/bin/bash
[...]
flag14:x:3014:3014::/home/flag/flag14:/bin/bash
```

```bash
(gdb) b *0x08048b0a
(gdb) c
(gdb) disas
Dump of assembler code for function main:
[...]
   0x08048afd <+439>:	call   0x80484b0 <getuid@plt>
   0x08048b02 <+444>:	mov    %eax,0x18(%esp)
   0x08048b06 <+448>:	mov    0x18(%esp),%eax
=> 0x08048b0a <+452>:	cmp    $0xbbe,%eax
(gdb) set $eax = 3014
(gdb) c
Continuing.
Check flag.Here is your token : 7QiHafiNa3HVozsaXkawuYrTstxbpABHD8CPnHJ
[Inferior 1 (process 2619) exited normally]
```

It worked !! We now have the flag !!!
We logged to flag14:

```bash
level14@SnowCrash:~$ su flag14
Password: 7QiHafiNa3HVozsaXkawuYrTstxbpABHD8CPnHJ
Congratulation. Type getflag to get the key and send it to me the owner of this livecd :)
```