# chrono #
 
 
## Description ##
 
How to automate tasks to run at intervals on linux servers?
 
## Thought process ##
 Cron is a time-based job scheduler in Linux operating systems, that allows you to automate tasks to run at specified intervals. "*crontab*" is The primary command used to manage cron jobs.

 After brief overview of the crontab help menu:

```bash
$ crontab --help
crontab: invalid option -- '-'
crontab: usage error: unrecognized option
usage:  crontab [-u user] file
    crontab [ -u user ] [ -i ] { -e | -l | -r }
        (default operation is replace, per 1003.2)
    -e  (edit user's crontab)
    -l  (list user's crontab)
    -r  (delete user's crontab)
    -i  (prompt before deleting user's crontab)
```

We try listing the user's (in this case picoplayer) crontab, which turns out to be empty:
```bash
$ crontab -l
no crontab for picoplayer
``` 

We look into the documentation of crontab to find that:
https://www.man7.org/linux/man-pages/man5/crontab.5.html
```text
FILES         top

       /etc/crontab main system crontab file.  /var/spool/cron/ a
       directory for storing crontabs defined by users.  /etc/cron.d/ a
       directory for storing system crontabs.
```

## Solution ##

We display the contents of system wide jobs:

```bash
$ cat /etc/crontab 
# picoCTF{...}
```