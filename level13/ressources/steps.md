When we started the level13 there is:
- A binary called **level13**

```bash
level13@SnowCrash:~$ ./level13
UID 2013 started us but we we expect 4242
```

The binary expect to be started with UID 4242. let's dive into it with gdb:

```bash
(gdb) break main
Breakpoint 1 at 0x804858f
(gdb) run
Starting program: /home/user/level13/level13 

Breakpoint 1, 0x0804858f in main ()
(gdb) disas
Dump of assembler code for function main:
   0x0804858c <+0>:	push   %ebp
   0x0804858d <+1>:	mov    %esp,%ebp
=> 0x0804858f <+3>:	and    $0xfffffff0,%esp
   0x08048592 <+6>:	sub    $0x10,%esp
   0x08048595 <+9>:	call   0x8048380 <getuid@plt>
   0x0804859a <+14>:	cmp    $0x1092,%eax # only one compare here
   0x0804859f <+19>:	je     0x80485cb <main+63>
   0x080485a1 <+21>:	call   0x8048380 <getuid@plt>
   0x080485a6 <+26>:	mov    $0x80486c8,%edx
   0x080485ab <+31>:	movl   $0x1092,0x8(%esp)
   0x080485b3 <+39>:	mov    %eax,0x4(%esp)
   0x080485b7 <+43>:	mov    %edx,(%esp)
   0x080485ba <+46>:	call   0x8048360 <printf@plt>
   0x080485bf <+51>:	movl   $0x1,(%esp)
   0x080485c6 <+58>:	call   0x80483a0 <exit@plt>
   0x080485cb <+63>:	movl   $0x80486ef,(%esp)
   0x080485d2 <+70>:	call   0x8048474 <ft_des>
   0x080485d7 <+75>:	mov    $0x8048709,%edx
   0x080485dc <+80>:	mov    %eax,0x4(%esp)
   0x080485e0 <+84>:	mov    %edx,(%esp)
   0x080485e3 <+87>:	call   0x8048360 <printf@plt>
   0x080485e8 <+92>:	leave  
   0x080485e9 <+93>:	ret    
End of assembler dump.
(gdb) 
```
we can see only one cmp instructions at line +14, just get to the line with **ni** for next instructions and print %eax:
```bash
(gdb) p $eax
$1 = 2013
```
we can modify eax to pass the compare:
```bash
(gdb) p $eax
$1 = 2013
(gdb) set $eax = 4242
(gdb) ni
0x0804859f in main ()
(gdb) 
0x080485cb in main ()
(gdb) 
0x080485d2 in main ()
(gdb) 
0x080485d7 in main ()
(gdb) 
0x080485dc in main ()
(gdb) 
0x080485e0 in main ()
(gdb) 
0x080485e3 in main ()
(gdb) 
your token is 2A31L79asukciNyi8uppkEuSx
0x080485e8 in main ()
(gdb) 
0x080485e9 in main ()
(gdb) 
```

Here the flag !
