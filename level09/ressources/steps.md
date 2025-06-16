When we started the level09, we can see two differents files:
- A binary called **level09**
- A file called **token**

The binary seems to transform the string passed as argument with a simple crypto algorithm:
"abc" will be "ace"

It just add the position of the char to it's ascii value.
```
a + 0 = a
b + 1 = c
b + 2 = e
```

After a bit of search, we can see with 
```bash
~$ strings level09
You should not reverse this
```

and we have a token ! it seems like the token has been crypted with the level09 binary so let's create a simple program that can reverse the level09 crypt algo:

```c
#include <stdio.h>
#include <string.h>
#include <unistd.h>

int main(int ac, char **av) {
    if (ac != 2)
        return (1);
    const unsigned char      *value = av[1];
    const size_t    str_size = strlen(av[1]);
    unsigned char             tmp[1000] = {0};

    for (int i = 0; i < str_size; ++i) {
        tmp[i] = value[i] - i;
    }

    printf("\nReversed string: %s\n", (const char *)tmp);
}
```

```bash
cd /tmp
vim main.c
cc -std=99 main.c
```

```bash
level09@SnowCrash:/tmp$ ./a.out `cat ~/token`

Reversed string: f3iji1ju5yuevaus41q1afiuq
```

and we get the password to flag09 !