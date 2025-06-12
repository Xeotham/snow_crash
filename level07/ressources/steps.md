When we started the level07, we can see the binary **level07**

it prints *level07*

so we try to change the filename in tmp, doesnt work.

in env we can see **LOGNAME=level07**
set it at getflag:
```bash
export LOGNAME='`getflag`'
```

execute ./level07 and you got the flag.