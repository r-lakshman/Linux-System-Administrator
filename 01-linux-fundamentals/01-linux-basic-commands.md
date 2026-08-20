# Linux Basic Commands

A practical reference for commonly used Linux commands related to user information, user switching, passwords, hostname management, date/time, uptime, directory navigation, file management, viewing, searching, redirection, and command history.

> **Note:** Example outputs are representative. Actual usernames, paths, dates, IP addresses, permissions, and command results will vary by system.

---

## Table of Contents

1. [Command Syntax](#1-command-syntax)
2. [User Information](#2-user-information)
3. [Password Management](#3-password-management)
4. [sudo and User Switching](#4-sudo-and-user-switching)
5. [User Management](#5-user-management)
6. [Login Sessions](#6-login-sessions)
7. [Hostname and System Information](#7-hostname-and-system-information)
8. [Date and Time](#8-date-and-time)
9. [System Uptime](#9-system-uptime)
10. [pwd](#10-pwd)
11. [ls](#11-ls)
12. [ll](#12-ll)
13. [cd](#13-cd)
14. [mkdir](#14-mkdir)
15. [touch](#15-touch)
16. [cat](#16-cat)
17. [echo](#17-echo)
18. [Redirection](#18-redirection)
19. [less](#19-less)
20. [head](#20-head)
21. [tail](#21-tail)
22. [truncate](#22-truncate)
23. [grep](#23-grep)
24. [wc](#24-wc)
25. [cp](#25-cp)
26. [mv](#26-mv)
27. [rm](#27-rm)
28. [rmdir](#28-rmdir)
29. [find](#29-find)
30. [history](#30-history)
31. [Important Path Symbols](#31-important-path-symbols)
32. [Important Options](#32-important-options)
33. [Quick Reference](#33-quick-reference)

---

# 1. Command Syntax

Linux commands generally follow:

```bash
command [options] [arguments]
```

| Part | Meaning |
|---|---|
| `command` | Command to execute |
| `[options]` | Optional flags that change behavior |
| `[arguments]` | Optional input such as a file, directory, or pattern |

Example:

```bash
ls
ls -l
ls /home/lakshman
ls -la /home/lakshman
```

---

# 2. User Information

## `id`

Displays UID, GID, and groups for a user.

```bash
id
```

Example output:

```text
uid=1000(lakshmanr) gid=1000(lakshmanr) groups=1000(lakshmanr),27(sudo)
```

## `whoami`

Displays the current username.

```bash
whoami
```

Example output:

```text
lakshmanr
```

If logged in as root:

```text
root
```

## `who`

Displays users currently logged into the system.

```bash
who
```

Example output:

```text
lakshmanr pts/0 2026-08-21 09:30 (192.168.1.10)
```

---

# 3. Password Management

## `passwd`

Changes the current user's password.

```bash
passwd
```

Example:

```text
Changing password for lakshmanr.
Current password:
New password:
Retype new password:
passwd: password updated successfully
```

## `passwd username`

Root can change another user's password:

```bash
passwd lakshmanr
```

Example:

```text
New password:
Retype new password:
passwd: password updated successfully
```

## `sudo passwd username`

A sudo-enabled user can change another user's password:

```bash
sudo passwd lakshmanr
```

Example:

```text
[sudo] password for administrator:
New password:
Retype new password:
passwd: password updated successfully
```

---

# 4. sudo and User Switching

## `sudo`

Runs a command with root privileges.

```bash
sudo hostnamectl
```

Example:

```text
[sudo] password for lakshmanr:
```

## `sudo -i`

Opens an interactive root login shell.

```bash
sudo -i
```

Example:

```text
lakshmanr@ubuntu:~$ sudo -i
[sudo] password for lakshmanr:
root@ubuntu:~#
```

Verify:

```bash
whoami
```

Output:

```text
root
```

Exit:

```bash
exit
```

## `su`

Switches to another user. Without a username, it normally attempts to switch to root.

```bash
su
```

Example:

```text
lakshmanr@ubuntu:~$ su
Password:
root@ubuntu:/home/lakshmanr#
```

## `su -`

Switches to root and loads the root user's login environment.

```bash
su -
```

Example:

```text
lakshmanr@ubuntu:~$ su -
Password:
root@ubuntu:~#
```

Verify:

```bash
whoami
```

Output:

```text
root
```

## `su - username`

Switches to a specific user with that user's login environment.

```bash
su - lakshmanr
```

Example:

```text
Password:
lakshmanr@ubuntu:~$
```

### `sudo -i` vs `su -`

| Command | Result | Password |
|---|---|---|
| `sudo -i` | Root shell | Current user's password |
| `su -` | Root shell | Root user's password |
| `su username` | Switch user | Target user's password |
| `su - username` | Login shell as user | Target user's password |

---

# 5. User Management

## `usermod -l`

Changes a user's login username.

```bash
sudo usermod -l newusername oldusername
```

Example:

```bash
sudo usermod -l lakshmanr lalkmanr
```

Normally there is no output when successful.

Verify:

```bash
id lakshmanr
```

Example output:

```text
uid=1000(lakshmanr) gid=1000(lalkmanr) groups=1000(lalkmanr),27(sudo)
```

> Avoid changing a username while that user is currently logged in.

---

# 6. Login Sessions

## `loginctl list-sessions`

Displays active login sessions.

```bash
loginctl list-sessions
```

Example output:

```text
SESSION UID  USER       SEAT TTY
1       1000 lakshmanr  -    pts/0
2       1000 lakshmanr  -    pts/1
```

---

# 7. Hostname and System Information

## `hostnamectl`

Displays hostname and system information.

```bash
hostnamectl
```

Example output:

```text
Static hostname: ubuntu-server
Icon name: computer-vm
Chassis: vm
Operating System: Ubuntu 24.04 LTS
Kernel: Linux 6.8.0
Architecture: x86-64
```

## `hostnamectl set-hostname`

Changes the hostname.

```bash
sudo hostnamectl set-hostname linux-server
```

Usually no output is produced when successful.

Verify:

```bash
hostnamectl
```

Example:

```text
Static hostname: linux-server
```

## `hostname`

Displays the hostname.

```bash
hostname
```

Output:

```text
linux-server
```

## `hostname -I`

Displays IP addresses assigned to the system.

```bash
hostname -I
```

Example output:

```text
192.168.1.25
```

---

# 8. Date and Time

## `date`

Displays the current date and time.

```bash
date
```

Example output:

```text
Fri Aug 21 09:35:20 IST 2026
```

## `date -u`

Displays UTC time.

```bash
date -u
```

Example:

```text
Fri Aug 21 05:05:20 UTC 2026
```

## `date +FORMAT`

Displays a custom date/time format.

Common formats:

| Format | Meaning |
|---|---|
| `%Y` | Year |
| `%m` | Month |
| `%d` | Day |
| `%H` | Hour |
| `%M` | Minute |
| `%S` | Second |

Example:

```bash
date "+%Y-%m-%d %H:%M:%S"
```

Output:

```text
2026-08-21 09:35:20
```

Other examples:

```bash
date "+%Y-%m-%d"
```

```text
2026-08-21
```

```bash
date "+%d-%m-%Y"
```

```text
21-08-2026
```

```bash
date "+%H:%M:%S"
```

```text
09:35:20
```

## `date -s`

Sets the system date/time.

```bash
sudo date -s "2026-08-21 10:30:00"
```

Example:

```text
Fri Aug 21 10:30:00 IST 2026
```

> NTP/time synchronization may change the time again.

## `timedatectl`

Displays local time, UTC, timezone, NTP status, and RTC information.

```bash
timedatectl
```

Example:

```text
Local time: Fri 2026-08-21 09:35:20 IST
Universal time: Fri 2026-08-21 04:05:20 UTC
RTC time: Fri 2026-08-21 04:05:20
Time zone: Asia/Kolkata (IST, +0530)
System clock synchronized: yes
NTP service: active
RTC in local TZ: no
```

## `timedatectl list-timezones`

Lists available timezones.

```bash
timedatectl list-timezones
```

Example:

```text
Asia/Kolkata
Asia/Dubai
Asia/Tokyo
Europe/London
America/New_York
```

## `timedatectl set-timezone`

Changes the timezone.

```bash
sudo timedatectl set-timezone Asia/Kolkata
```

Verify:

```bash
timedatectl
```

Example:

```text
Time zone: Asia/Kolkata (IST, +0530)
```

## `timedatectl set-ntp`

Enable NTP:

```bash
sudo timedatectl set-ntp true
```

Disable NTP:

```bash
sudo timedatectl set-ntp false
```

Verify:

```bash
timedatectl
```

Example:

```text
System clock synchronized: yes
NTP service: active
```

---

# 9. System Uptime

## `uptime`

Shows current time, uptime, logged-in users, and load average.

```bash
uptime
```

Example output:

```text
09:35:20 up 2 days, 4:15, 2 users, load average: 0.10, 0.08, 0.05
```

## `uptime -s`

Shows the last boot/start time.

```bash
uptime -s
```

Example:

```text
2026-08-19 05:20:15
```

---

# 10. pwd

## `pwd` — Print Working Directory

Displays the absolute path of the current working directory.

```bash
pwd
```

Example output:

```text
/home/lakshman/linux-admin
```

**Remember:** `pwd` → Shows where you are.

---

# 11. ls

## `ls` — List Files and Directories

```bash
ls
```

Example output:

```text
file1.txt
file2.txt
projects
```

### Common Options

| Option | Meaning |
|---|---|
| `-a` | Show hidden files |
| `-l` | Long/detailed listing |
| `-h` | Human-readable sizes |
| `-R` | Recursive listing |
| `-d` | Show directory itself |
| `-t` | Sort by modification time |
| `-S` | Sort by file size |
| `-r` | Reverse sort order |

## `ls -a`

Shows hidden files.

```bash
ls -a
```

Example:

```text
.
..
.bashrc
.config
file.txt
projects
```

`.` = current directory  
`..` = parent directory

## `ls -l`

Long/detailed listing.

```bash
ls -l
```

Example:

```text
-rw-r--r-- 1 lakshmanr lakshmanr 125 Aug 21 09:30 file1.txt
drwxr-xr-x 2 lakshmanr lakshmanr  40 Aug 21 09:20 projects
```

Shows permissions, links, owner, group, size, modification date/time, and name.

## `ls -la`

Detailed listing including hidden files.

```bash
ls -la
```

Example:

```text
drwxr-xr-x 4 lakshmanr lakshmanr 4096 Aug 21 09:30 .
drwxr-xr-x 6 lakshmanr lakshmanr 4096 Aug 21 09:00 ..
-rw-r--r-- 1 lakshmanr lakshmanr  220 Aug 21 09:00 .bashrc
-rw-r--r-- 1 lakshmanr lakshmanr   25 Aug 21 09:30 file1.txt
```

## `ls -lh`

Long listing with human-readable sizes.

```bash
ls -lh
```

Example:

```text
-rw-r--r-- 1 lakshmanr lakshmanr 2.5K Aug 21 09:30 file.txt
```

## `ls -R`

Lists directories recursively.

```bash
ls -R
```

Example:

```text
.
file1.txt
projects

./projects:
app.txt
notes.txt
```

## `ls -t`

Sorts by modification time, newest first.

```bash
ls -lt
```

Example:

```text
-rw-r--r-- 1 lakshmanr lakshmanr  50 Aug 21 10:10 new.txt
-rw-r--r-- 1 lakshmanr lakshmanr 100 Aug 21 09:30 file.txt
```

## `ls -ltr` — Long Listing, Time Sorted, Reverse Order

This is especially useful when you want the **oldest modified files first**.

```bash
ls -ltr
```

Breakdown:

```text
-l  → Long/detailed listing
-t  → Sort by modification time
-r  → Reverse the order
```

Example output:

```text
-rw-r--r-- 1 lakshmanr lakshmanr  80 Aug 20 08:15 old.txt
-rw-r--r-- 1 lakshmanr lakshmanr 120 Aug 20 15:40 report.txt
-rw-r--r-- 1 lakshmanr lakshmanr 250 Aug 21 09:30 new.txt
```

**Remember:**

```text
ls -lt   → Newest first
ls -ltr  → Oldest first
```

---

# 12. ll

`ll` is commonly configured as an alias for:

```bash
ls -l
```

Example:

```bash
ll
```

Output:

```text
-rw-r--r-- 1 lakshmanr lakshmanr 125 Aug 21 09:30 file1.txt
drwxr-xr-x 2 lakshmanr lakshmanr  40 Aug 21 09:20 projects
```

Check whether it exists:

```bash
alias ll
```

Example:

```text
alias ll='ls -l'
```

> `ll` is usually an alias and may not exist on every Linux system.

---

# 13. cd

## `cd` — Change Directory

```bash
cd [directory]
```

| Command | Meaning |
|---|---|
| `cd folder` | Enter directory |
| `cd .` | Current directory |
| `cd ..` | Parent directory |
| `cd ../folder` | Go through parent into another directory |
| `cd ~` | Home directory |
| `cd /` | Root directory |
| `cd -` | Previous working directory |
| `cd` | Home directory |

## `cd .`

```bash
cd .
pwd
```

Example:

```text
/home/lakshman/lk
```

## `cd ..`

```bash
cd ..
pwd
```

Example:

```text
/home/lakshman
```

## `cd ../rlk`

If currently in `/home/lakshman/lk`:

```bash
cd ../rlk
pwd
```

Output:

```text
/home/lakshman/rlk
```

## `cd ~`

```bash
cd ~
pwd
```

Output:

```text
/home/lakshman
```

## `cd /`

```bash
cd /
pwd
```

Output:

```text
/
```

## `cd -`

```bash
cd -
```

Example output:

```text
/home/lakshman/rlk
```

---

# 14. mkdir

Creates directories.

```bash
mkdir [options] directory_name
```

Common options:

| Option | Meaning |
|---|---|
| `-p` | Create parent directories |
| `-v` | Show what is created |
| `-m` | Set directory permissions |

## Create one directory

```bash
mkdir projects
```

Example:

```text
# No output on success
```

## Create multiple directories

```bash
mkdir folder1 folder2 folder3
```

## Brace expansion

```bash
mkdir folder{1..3}
```

Creates:

```text
folder1
folder2
folder3
```

## `mkdir -p`

```bash
mkdir -p parent/child/grandchild
```

Creates the complete directory structure.

Example verification:

```bash
find parent -type d
```

Output:

```text
parent
parent/child
parent/child/grandchild
```

---

# 15. touch

Creates an empty file or updates timestamps.

```bash
touch file.txt
```

Example:

```bash
ls -l file.txt
```

Output:

```text
-rw-r--r-- 1 lakshmanr lakshmanr 0 Aug 21 10:00 file.txt
```

Create multiple files:

```bash
touch file1.txt file2.txt file3.txt
```

Create 10 files:

```bash
touch file{1..10}
```

Creates:

```text
file1
file2
file3
...
file10
```

---

# 16. cat

Displays file contents.

```bash
cat file.txt
```

Example:

```text
Hello Linux
Welcome to Linux administration
```

## `cat -n`

Shows line numbers.

```bash
cat -n file.txt
```

Output:

```text
     1  Hello Linux
     2  Welcome to Linux administration
```

## Copy contents using `>`

```bash
cat file1.txt > file2.txt
```

`>` overwrites `file2.txt`.

## Append using `>>`

```bash
cat file1.txt >> file2.txt
```

`>>` appends to `file2.txt`.

---

# 17. echo

Prints text or variable values.

```bash
echo "Hello, World!"
```

Output:

```text
Hello, World!
```

## `echo -e`

Enables escape sequences.

```bash
echo -e "Hello\nWorld"
```

Output:

```text
Hello
World
```

Common escape characters:

| Escape | Meaning |
|---|---|
| `\n` | New line |
| `\t` | Tab |
| `\\` | Backslash |
| `\a` | Alert |
| `\b` | Backspace |

---

# 18. Redirection

## `>` — Overwrite

```bash
echo "Linux" > file.txt
```

If the file contained:

```text
Hello
World
```

After the command:

```text
Linux
```

`>` creates a file if it does not exist and overwrites it if it exists.

## `>>` — Append

```bash
echo "DevOps" >> file.txt
```

If the file contains:

```text
Linux
```

After:

```text
Linux
DevOps
```

## `|` — Pipe

Sends the output of one command to another command.

```bash
ls -l | grep ".txt"
```

Example output:

```text
-rw-r--r-- 1 lakshmanr lakshmanr 120 Aug 21 09:30 file.txt
```

---

# 19. less

Views a file one screen at a time.

```bash
less file.txt
```

Useful keys:

| Key | Meaning |
|---|---|
| `Space` | Next page |
| `b` | Previous page |
| `↑` | Move up |
| `↓` | Move down |
| `/text` | Search |
| `n` | Next match |
| `N` | Previous match |
| `q` | Quit |

Examples:

```bash
less -N file.txt
less -S file.txt
less -i file.txt
```

---

# 20. head

Shows the beginning of a file.

Default: first 10 lines.

```bash
head file.txt
```

Example output:

```text
Line 1
Line 2
Line 3
Line 4
Line 5
Line 6
Line 7
Line 8
Line 9
Line 10
```

First 5 lines:

```bash
head -5 file.txt
```

or:

```bash
head -n 5 file.txt
```

---

# 21. tail

Shows the end of a file.

Default: last 10 lines.

```bash
tail file.txt
```

Last 5 lines:

```bash
tail -5 file.txt
```

Follow a log file:

```bash
tail -f logfile.txt
```

Example:

```text
2026-08-21 10:01:02 INFO Application started
2026-08-21 10:01:05 INFO User connected
```

Stop `tail -f` with:

```text
Ctrl + C
```

---

# 22. truncate

Changes the size of a file.

## Empty a file

```bash
truncate -s 0 file.txt
```

Verify:

```bash
ls -l file.txt
```

Example:

```text
-rw-r--r-- 1 lakshmanr lakshmanr 0 Aug 21 10:05 file.txt
```

## Set file size

```bash
truncate -s 5 file.txt
```

Verify:

```bash
ls -l file.txt
```

Example:

```text
-rw-r--r-- 1 lakshmanr lakshmanr 5 Aug 21 10:06 file.txt
```

---

# 23. grep

Searches for matching text.

```bash
grep "Lakshman" file.txt
```

Example output:

```text
Hello Lakshman
Lakshman is learning Linux
```

## `grep -i`

Ignore case:

```bash
grep -i "lakshman" file.txt
```

## `grep -n`

Show line numbers:

```bash
grep -n "Lakshman" file.txt
```

Example:

```text
2:Hello Lakshman
5:Lakshman is learning Linux
```

## `grep -o`

Show only matching text:

```bash
grep -o "Lakshman" file.txt
```

Output:

```text
Lakshman
Lakshman
```

## `grep -v`

Show lines that do not match:

```bash
grep -v "Lakshman" file.txt
```

## `grep -c`

Count matching lines:

```bash
grep -c "Lakshman" file.txt
```

Output:

```text
2
```

## `grep -r`

Search recursively:

```bash
grep -r "Lakshman" /home/lakshman/
```

## Combine options

```bash
grep -o -i -n "text" file.txt
```

---

# 24. wc

Counts lines, words, bytes, and characters.

```bash
wc file.txt
```

Example:

```text
5 12 85 file.txt
```

Meaning:

```text
5   → lines
12  → words
85  → bytes
```

Commands:

```bash
wc -l file.txt
wc -w file.txt
wc -c file.txt
wc -m file.txt
```

Example:

```bash
wc -l file.txt
```

Output:

```text
5 file.txt
```

---

# 25. cp

Copies files and directories.

```bash
cp [options] source destination
```

## Copy a file

```bash
cp file.txt backup.txt
```

Example:

```bash
ls
```

Output:

```text
backup.txt
file.txt
```

## Copy a file to a directory

```bash
cp file.txt /home/user/Documents/
```

## Copy directory

```bash
cp -r source_folder destination_folder
```

## Archive copy

```bash
cp -a source_folder destination_folder
```

## Interactive

```bash
cp -i file.txt backup.txt
```

Example:

```text
cp: overwrite 'backup.txt'? y
```

## Verbose

```bash
cp -v file.txt backup.txt
```

Example:

```text
'file.txt' -> 'backup.txt'
```

---

# 26. mv

Moves or renames files/directories.

## Rename

```bash
mv old.txt new.txt
```

Example:

```bash
ls
```

Output:

```text
new.txt
```

## Move file

```bash
mv file.txt /home/user/Documents/
```

## Move directory

```bash
mv folder1 /tmp/
```

## Interactive

```bash
mv -i file.txt /tmp/
```

Example:

```text
mv: overwrite '/tmp/file.txt'? y
```

## Verbose

```bash
mv -v file.txt /tmp/
```

Example:

```text
renamed 'file.txt' -> '/tmp/file.txt'
```

---

# 27. rm

Removes files and directories.

## Remove file

```bash
rm file.txt
```

Normally no output on success.

## Remove multiple files

```bash
rm file1.txt file2.txt
```

## Remove directory

```bash
rm -r folder
```

## Force recursive removal

```bash
rm -rf folder
```

Breakdown:

```text
-r  → Recursive
-f  → Force
-rf → Recursive + Force
```

## Interactive

```bash
rm -i file.txt
```

Example:

```text
rm: remove regular file 'file.txt'? y
```

## Verbose

```bash
rm -v file.txt
```

Example:

```text
removed 'file.txt'
```

> **Warning:** `rm -rf` can permanently delete data. Use it carefully.

---

# 28. rmdir

Removes an empty directory.

```bash
rmdir projects
```

No output normally means success.

For nested empty directories:

```bash
rmdir -p parent/child
```

`rmdir` only removes empty directories.

---

# 29. find

Searches for files and directories.

```bash
find [path] [options] [expression]
```

## Find a file

```bash
find . -name "file.txt"
```

Example:

```text
./documents/file.txt
```

## Find `.log` files

```bash
find . -name "*.log"
```

Example:

```text
./logs/app.log
./logs/error.log
```

## Find files

```bash
find . -type f
```

Example:

```text
./file1.txt
./documents/report.txt
```

## Find directories

```bash
find . -type d
```

Example:

```text
.
./documents
./projects
```

## Case-insensitive search

```bash
find . -iname "file.txt"
```

## Limit search depth

```bash
find . -maxdepth 2 -name "*.txt"
```

Common options:

| Option | Meaning |
|---|---|
| `-name` | Search by name |
| `-iname` | Search by name, ignoring case |
| `-type f` | Find files |
| `-type d` | Find directories |
| `-size` | Search by size |
| `-mtime` | Search by modification time |
| `-user` | Search by owner |
| `-perm` | Search by permissions |
| `-maxdepth` | Limit search depth |
| `-exec` | Execute command on results |

---

# 30. history

Displays previously executed commands.

```bash
history
```

Example:

```text
103  cat file.txt
104  pwd
105  ls -la
```

## Last 10 commands

```bash
history 10
```

## Search history

```bash
history | grep terraform
```

Example:

```text
87  terraform init
92  terraform plan
```

## Run a command by history number

```bash
!103
```

Runs:

```bash
cat file.txt
```

## Run previous command

```bash
!!
```

## Clear history

```bash
history -c
```

---

# 31. Important Path Symbols

| Symbol | Meaning | Example |
|---|---|---|
| `.` | Current directory | `cd .` |
| `..` | Parent directory | `cd ..` |
| `~` | Home directory | `cd ~` |
| `/` | Root directory | `cd /` |
| `*` | Wildcard | `rm *.txt` |

---

# 32. Important Options

These meanings are common but command-specific.

| Option | Common Meaning |
|---|---|
| `-a` | All / hidden files / archive |
| `-l` | Long/detailed listing |
| `-h` | Human-readable |
| `-r` | Recursive / reverse depending on command |
| `-R` | Recursive |
| `-f` | Force |
| `-i` | Interactive / ignore case depending on command |
| `-v` | Verbose |
| `-n` | Number / no newline depending on command |
| `-p` | Parent / preserve depending on command |
| `-c` | Count / bytes depending on command |
| `-o` | Output only / command-specific |
| `-d` | Directory / date / command-specific |

**Important:** Options are command-specific.

For example:

```text
grep -i → Ignore case
rm -i   → Ask for confirmation
```

Check available options:

```bash
command --help
```

Examples:

```bash
ls --help
cp --help
rm --help
grep --help
```

---

# 33. Quick Reference

| Command | Purpose |
|---|---|
| `id` | Show UID, GID, and groups |
| `whoami` | Show current username |
| `who` | Show logged-in users |
| `passwd` | Change password |
| `sudo` | Run command with root privileges |
| `sudo -i` | Open root login shell |
| `su` | Switch user |
| `su -` | Switch to root with login environment |
| `su - username` | Switch to another user |
| `usermod -l` | Change username |
| `loginctl list-sessions` | Show active sessions |
| `hostnamectl` | Show hostname/system information |
| `hostname` | Show hostname |
| `hostname -I` | Show IP addresses |
| `date` | Show current date/time |
| `date -u` | Show UTC time |
| `date +FORMAT` | Show custom date/time |
| `timedatectl` | Show time/timezone/NTP information |
| `uptime` | Show system uptime |
| `uptime -s` | Show last boot time |
| `pwd` | Show current directory |
| `ls` | List files/directories |
| `ls -l` | Detailed listing |
| `ls -la` | Detailed + hidden files |
| `ls -lh` | Human-readable listing |
| `ls -lt` | Newest modified files first |
| `ls -ltr` | **Oldest modified files first** |
| `ll` | Common alias for `ls -l` |
| `cd` | Change directory |
| `mkdir` | Create directory |
| `touch` | Create file/update timestamp |
| `cat` | Display file |
| `echo` | Print text |
| `less` | View file page by page |
| `head` | Show beginning of file |
| `tail` | Show end of file |
| `truncate` | Resize/empty file |
| `grep` | Search text |
| `wc` | Count lines/words/bytes |
| `cp` | Copy |
| `mv` | Move/rename |
| `rm` | Remove |
| `rmdir` | Remove empty directory |
| `find` | Search files/directories |
| `history` | Show command history |

---

# Key Points to Remember

```text
.       → Current directory
..      → Parent directory
~       → Home directory
/       → Root directory
*       → Wildcard

>       → Overwrite
>>      → Append
|       → Pipe

-r      → Recursive
-f      → Force
-rf     → Recursive + Force
-l      → Long listing
-a      → All / hidden files
-h      → Human-readable
-v      → Verbose
-i      → Command-specific
```

### `ls` Sorting Shortcut

```text
ls -lt   → Newest modified first
ls -ltr  → Oldest modified first
```

### Practical Command Flow

```bash
# Check current location
pwd

# List files
ls

# Detailed listing
ls -l

# Oldest modified files first
ls -ltr

# List hidden files
ls -la

# Create a directory
mkdir project

# Enter directory
cd project

# Create 3 files
touch file{1..3}

# Check files
ls -l

# Add content
echo "Hello Linux" > file1

# Display content
cat file1

# Search text
grep -n "Linux" file1

# Copy file
cp file1 file1-backup

# Rename file
mv file1-backup backup.txt

# Display files
ls -l

# Go back
cd ..

# Check location
pwd
```

> **Best practice:** Do not memorize every option. Learn the common options and use `command --help` whenever you need to verify an option.

---

## Navigation

[🏠 Back to Home](https://r-lakshman.github.io/Linux-System-Administrator/) | [View on GitHub](https://github.com/r-lakshman/Linux-System-Administrator/blob/main/01-linux-fundamentals/01-linux-basic-commands.md) | [Next: Terminal Keyboard Shortcuts →](https://r-lakshman.github.io/Linux-System-Administrator/01-linux-fundamentals/02-terminal-keyboard-shortcuts.html)

---

© 2026 R Lakshman Kumar. All rights reserved.

