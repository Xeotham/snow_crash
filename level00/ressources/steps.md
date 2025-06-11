First, we verified which files the user flagg00 had permissions for.
For this, we used the cmd:

```bash
find / -user flag00
```

which gave us the file:

```bash
/rofs/usr/sbin/john
```

With the content:
**cdiiddwpgswtgt**

We used [a ceasar decoder](https://www.dcode.fr/chiffre-cesar)

To check Ceasar's cipher we get "nottoohardhere"

Which is the password for flag00.
