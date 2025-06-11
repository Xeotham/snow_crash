In search of the password we try to see the passwd file with:

```bash
cat /etc/passwd
```

and we noticed this line:

```bash
flag01:42hDRfypTqqnw:3001:3001::/home/flag/flag01:/bin/bash
```

the **42hDRfypTqqnw** is the password and we can see it's not encrypted in the shadow file. In tutorial [video](https://elearning.intra.42.fr/notions/127/subnotions/465/videos/404) it talk about [john](hhttps://github.com/openwall/john://github.com/openwall/john) to decrypt password.

We give the file **/etc/passwd** to john and it give us the password:

```bash
abcdefg
```