# See the `ENV` of a running process

To check what `ENV` vars a process is running with (on Linux):

```
% cat /proc/1156/environ | tr '\0' '\n'
LANG=en_US.UTF-8
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
HOME=/home/user
LOGNAME=user
USER=user
SHELL=/bin/bash
INVOCATION_ID=ab9efdd564e14a1e83237b1db29607cd
JOURNAL_STREAM=8:49432749
PYTHONPATH=/var/user/python
PYTHONDONTWRITEBYTECODE=1
```
