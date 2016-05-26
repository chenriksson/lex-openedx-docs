#Tutorials: Linux for Windows Developers

##Command comparison:

| DOS              | Bash                  | Details |
| :--------------- | :-------------------- | :-----  |
| appwiz.cpl       | dpkg                  | `dpkg -l` to show installed packages |
| attrib           | chmod                 |         |
| cd               | cd, pwd               |         |
| cls              | clear                 |         |
| copy             | cp                    |         |
| date, time       | date                  |         |
| del              | rm                    |         |
| dir              | ls                    |  '-a' (all) to show hidden, '-l' (long) to show permissions |
| doskey (history) | history, !(bang)      | `!!` to run last, `!{prefix}` to run last matching, `!{num}` to run command number (from `history`) |
| doskey (macros)  | alias                 | i.e., `alias myhost=ssh user@myhost -i ~/.ssh/mykeyfile` |
| echo             | echo                  |         |
| eventvwr.msc     | {syslog}              |         |
| exit             | exit                  |         |
| {explorer/disk}  | df, du                | `df -h /` to show disk usage from root, `du --max-depth 1 ` |
| find             | grep                  | '-i' to ignore case, '-c' to show count, '-r' for recursive |
| fc/diff          | diff                  | `diff -qr {dir1} {dir2}` for recursive |
| (help) /?        | man {cmd}             | see: http://manpages.ubuntu.com |
| ipconfig         | /sbin/ifconfig        | View local IP address |
| mem              | free                  |         |
| mkdir            | mkdir                 |         |
| more             | cat, more, less, tail | `cat {file}` to show all, `more {file}` to page, `tail -f {file}` to continuously watch |
| move, ren        | mv                    |         |
| netstat          | netstat               | `sudo netstat lnptu` to display ports in use |
| runas            | su, sudo              | `su - {user}` to switch user, `sudo -u {user} {cmd}` to run as user, `sudo {cmd}` to run command as superuser |
| services.msc     | service               | <code>service {name} {start&#124;restart&#124;stop&#124;status}</code>, `service --status-all`, or `ls /etc/init.d` to see installed services |
| set              | env                   | `A=B` to set, `export A=B` to set globally |
| taskmgr.exe      | ps                    | `ps aux` or `ps -ef` to see all system processes, `ps -ejH` to see process tree |
| where            | which                 |         |
| winver           | lsb_release -a        | Display Linux version |
| (zip)            | tar                   | `tar cvf {*.tar.gz} {target}` to create, `tar xvf {*.tar.gz}` to extract |
| {*.msi}          | apt-get               | APT (Advanced Packaging Tool) package manager |

##File System:
    * File encoding: UTF-8 (Windows Unicode is UTF-16LE)
    * EOL delimiter: '\n' (Windows EOL is '\r\n')
    * Path delimiter: '/'
        * Note drive format for Git-Bash paths: "/c/Windows"
    * System directories:
        * /bin - common executables
        * /etc - system configuration files
        * /home - home directories
        * /root - administrative user's home
        * /tmp - temporary space, cleaned on reboot
        * /usr - programs, libraries, documentation
        * /var - storage for variable, temporary files (logs, mail queue, downloads, etc)
    * Permissions:
        * Symbolic notation: "-rwx|rwx|rwx"
            * '-' is file type. '-' for regular file, 'd' for directory, 'l' for symbolic link, etc.
            * 'rwx' denotes read, write, execute permissions
            * Permission triads are: owner|group|others
        * Numeric notation: (octal)
            * `stat -c %a {file}` to see numeric
            * Each digit is sum of its component bits
                * Binary: 100=read, 010=write, 001=execute
                * e.g.: 7=rwx, 6=rw, 5=rx, 4=r, 3=wx, 2=w, 1=x
                * e.g.: 777=rwx for everyone; 744=rwx for owner and r for everyone
    * Editors:
        * Nano (easier)
        * Vi (more powerful)
        * Notepad++ (SFTP) (remote)
    
Shell / Environment
    * (GNU) Bash is the default for Ubuntu, Git for Windows
        ○ i.e., versus Bourne (sh), Korn (ksh), C (csh), etc
    * Common variables
        * $USER
        * $PATH, $MANPATH
        * $SHELL
    * Profile
        * ~/.bash_profile

System Logging (SysLog)
    * Configuration:
        * Primary config: /etc/rsyslog.conf
        * Program config files: /etc/rsyslog.d
More information: Rsyslog