# Linux System Administrator

Linux system administration notes, commands, shortcuts, and practical guides.

--

**Home:** [🏠 README](https://r-lakshman.github.io/Linux-System-Administrator/)

**Next:** [Terminal Keyboard Shortcuts →](https://r-lakshman.github.io/Linux-System-Administrator/01-linux-fundamentals/02-terminal-keyboard-shortcuts.html)
---

# Linux Basic Commands

A practical reference for commonly used Linux commands related to user information, user switching, passwords, hostname management, date and time, and system uptime.

---

## 📑 Contents

1. [User Information](#user-information)
2. [User and Password Management](#user-and-password-management)
3. [User Switching and Privileges](#user-switching-and-privileges)
4. [User Management](#user-management)
5. [Login Sessions](#login-sessions)
6. [Hostname and System Information](#hostname-and-system-information)
7. [Linux Date and Time Commands](#linux-date-and-time-commands)
8. [Linux System Uptime Commands](#linux-system-uptime-commands)
9. [Password Rules](#password-rules)
10. [Quick Revision](#quick-revision)

---

# User Information

## `id`

- Displays information about a user.
- Shows:
  - **UID** → User ID
  - **GID** → Group ID
  - **Groups** → Groups the user belongs to.
- By default, it displays information about the current user.

### Command

```bash
id
````

### Output

```text
uid=1000(lakshmanr) gid=1000(lakshmanr) groups=1000(lakshmanr),27(sudo)
```

---

## `whoami`

* Displays the username of the current user.

### Command

```bash
whoami
```

### Output

```text
lakshmanr
```

If you are logged in as root:

```bash
whoami
```

Output:

```text
root
```

---

## `who`

* Displays users who are currently logged into the system.
* Shows the username, terminal, login time, and remote host when available.

### Command

```bash
who
```

### Output

```text
lakshmanr pts/0 2026-08-21 09:30 (192.168.1.10)
```

---

# User and Password Management

## `passwd`

* Used to change the password of the current user.
* Enter the current password first.
* Then enter and confirm the new password.

### Command

```bash
passwd
```

### Output

```text
Changing password for lakshmanr.
Current password:
New password:
Retype new password:
passwd: password updated successfully
```

---

## `passwd username`

* Used by root to change another user's password.
* If you are already root, you don't need `sudo`.
* Root does not need to know the user's old password.

### Example

```bash
passwd lakshmanr
```

### Output

```text
New password:
Retype new password:
passwd: password updated successfully
```

---

## `sudo passwd username`

* Used by a sudo-enabled user to change another user's password.
* `sudo` asks for your current user's password.
* `passwd` then asks for the new password of the target user.

### Example

```bash
sudo passwd lakshmanr
```

### Output

```text
[sudo] password for administrator:
New password:
Retype new password:
passwd: password updated successfully
```

If you are already root:

```bash
passwd lakshmanr
```

---

# User Switching and Privileges

## `sudo`

* Stands for **SuperUser Do**.
* Allows an authorized user to run a command with root privileges.
* Normally asks for the current user's password.
* It does not normally ask for the root password.

### Example

```bash
sudo hostnamectl
```

### Output

```text
[sudo] password for lakshmanr:
```

If you are already logged in as root, you don't need to use `sudo`.

---

## `sudo -i`

* Opens an interactive root login shell.
* The current user must have sudo privileges.
* Uses the current user's password.
* It normally does not require the root password.

### Command

```bash
sudo -i
```

### Output

```text
lakshmanr@ubuntu:~$ sudo -i
[sudo] password for lakshmanr:
root@ubuntu:~#
```

### Verify

```bash
whoami
```

Output:

```text
root
```

After becoming root, you don't need `sudo`:

```bash
hostnamectl
```

```bash
passwd lakshmanr
```

### Exit the root shell

```bash
exit
```

---

## `su`

* Stands for **Switch User**.
* Used to switch from the current user to another user.
* By default, it attempts to switch to root.
* Normally requires the root user's password.

### Command

```bash
su
```

### Output

```text
lakshmanr@ubuntu:~$ su
Password:
root@ubuntu:/home/lakshmanr#
```

---

## `su -`

* Switches to the root user.
* The `-` loads the root user's login environment.
* Requires the root user's password.

### Command

```bash
su -
```

### Output

```text
lakshmanr@ubuntu:~$ su -
Password:
root@ubuntu:~#
```

### Verify

```bash
whoami
```

Output:

```text
root
```

### Exit

```bash
exit
```

---

## `su - username`

* Switches to a specific user.
* The `-` loads the target user's login environment.
* Requires the target user's password.

### Example

```bash
su - lakshmanr
```

### Output

```text
Password:
lakshmanr@ubuntu:~$
```

---

## Difference Between `sudo -i` and `su -`

Both provide a root shell. The main difference is the password used.

### `sudo -i`

```text
sudo -i
    ↓
Current user's password
    ↓
Root shell
```

### `su -`

```text
su -
    ↓
Root user's password
    ↓
Root shell
```

| Command         | Result              | Password                |
| --------------- | ------------------- | ----------------------- |
| `sudo -i`       | Root shell          | Current user's password |
| `su -`          | Root shell          | Root user's password    |
| `su username`   | Switch to user      | Target user's password  |
| `su - username` | Login shell as user | Target user's password  |

> `sudo -i` requires sudo privileges.
> `su -` requires the root account/password to be available.

---

# User Management

## `usermod -l`

* Used to change a user's login username.

### Syntax

```bash
sudo usermod -l newusername oldusername
```

If you are already root:

```bash
usermod -l newusername oldusername
```

### Example

```bash
usermod -l lakshmanr lalkmanr
```

Changes:

```text
lalkmanr → lakshmanr
```

Normally produces no output when successful.

### Verify

```bash
id lakshmanr
```

Example output:

```text
uid=1000(lakshmanr) gid=1000(lalkmanr) groups=1000(lalkmanr),27(sudo)
```

> **Note:** Avoid changing a username while that user is currently logged in.

---

# Login Sessions

## `loginctl list-sessions`

* Displays the active login sessions on the system.
* Useful for checking whether a user is currently logged in.

### Command

```bash
loginctl list-sessions
```

### Output

```text
SESSION UID USER SEAT TTY
1       1000 lakshmanr -    pts/0
2       1000 lakshmanr -    pts/1
```

---

# Hostname and System Information

## `hostnamectl`

* Displays information about the system hostname.
* Also displays:

  * Operating system
  * Kernel
  * Architecture
  * Hostname

### Command

```bash
hostnamectl
```

### Output

```text
Static hostname: ubuntu-server
Icon name: computer-vm
Chassis: vm
Operating System: Ubuntu 24.04 LTS
Kernel: Linux 6.8.0
Architecture: x86-64
```

---

## `hostnamectl set-hostname`

* Used to change the system hostname.

### Normal sudo user

```bash
sudo hostnamectl set-hostname linux-server
```

### Root user

```bash
hostnamectl set-hostname linux-server
```

Normally produces no output when successful.

### Verify

```bash
hostnamectl
```

Output:

```text
Static hostname: linux-server
```

You can also use:

```bash
hostname
```

Output:

```text
linux-server
```

---

## `hostname -I`

* Displays the IP address or addresses assigned to the system.

### Command

```bash
hostname -I
```

### Output

```text
192.168.1.25
```

---

# Linux Date and Time Commands

## `date`

* Displays the current date and time.
* Uses the system's configured timezone.

### Command

```bash
date
```

### Output

```text
Fri Aug 21 09:35:20 IST 2026
```

### Change Date and Time

Normal sudo user:

```bash
sudo date -s "2026-08-21 10:30:00"
```

Root user:

```bash
date -s "2026-08-21 10:30:00"
```

### Output

```text
Fri Aug 21 10:30:00 IST 2026
```

> **Note:** NTP may automatically change the time back if time synchronization is enabled.

---

## `date -u`

* Displays the current date and time in UTC.
* `-u` means UTC.

### Command

```bash
date -u
```

### Output

```text
Fri Aug 21 05:05:20 UTC 2026
```

---

## `date +FORMAT`

* Displays date and time in a custom format.

### Common formats

* `%Y` → Year
* `%m` → Month
* `%d` → Day
* `%H` → Hour
* `%M` → Minute
* `%S` → Second

### Command

```bash
date "+%Y-%m-%d %H:%M:%S"
```

### Output

```text
2026-08-21 09:35:20
```

### Examples

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

---

## `timedatectl`

Displays:

* Local date and time
* UTC time
* Timezone
* NTP synchronization status
* Hardware clock information

### Command

```bash
timedatectl
```

### Output

```text
Local time: Fri 2026-08-21 09:35:20 IST
Universal time: Fri 2026-08-21 04:05:20 UTC
RTC time: Fri 2026-08-21 04:05:20
Time zone: Asia/Kolkata (IST, +0530)
System clock synchronized: yes
NTP service: active
RTC in local TZ: no
```

---

## `timedatectl list-timezones`

* Displays all available system timezones.

### Command

```bash
timedatectl list-timezones
```

### Output example

```text
Asia/Kolkata
Asia/Dubai
Asia/Tokyo
Europe/London
America/New_York
```

---

## `timedatectl set-timezone`

* Used to change the system timezone.

### Normal sudo user

```bash
sudo timedatectl set-timezone Asia/Kolkata
```

### Root user

```bash
timedatectl set-timezone Asia/Kolkata
```

### Verify

```bash
timedatectl
```

Example:

```text
Time zone: Asia/Kolkata (IST, +0530)
```

---

## `timedatectl set-ntp`

* Used to enable or disable network time synchronization.

### Enable NTP

```bash
sudo timedatectl set-ntp true
```

### Disable NTP

```bash
sudo timedatectl set-ntp false
```

If you are already root, don't use `sudo`.

### Verify

```bash
timedatectl
```

Example:

```text
System clock synchronized: yes
NTP service: active
```

---

# Linux System Uptime Commands

## `uptime`

* Shows how long the system has been running since the last boot.
* Also displays:

  * Current time
  * System uptime
  * Number of logged-in users
  * Load average

### Command

```bash
uptime
```

### Output

```text
09:35:20 up 2 days, 4:15, 2 users, load average: 0.10, 0.08, 0.05
```

---

## `uptime -s`

* Shows the date and time when the system was last started.

### Command

```bash
uptime -s
```

### Output

```text
2026-08-19 05:20:15
```

---

# Password Rules

## Change Your Own Password

```bash
passwd
```

* Enter your current password.
* Then enter the new password.

---

## Change Another User's Password with `sudo`

```bash
sudo passwd username
```

* `sudo` asks for your password.
* `passwd` sets the new password for the target user.

---

## Change Another User's Password as Root

```bash
passwd username
```

* No `sudo` is required.
* Root does not need the user's old password.

---

## Become Root with `sudo`

```bash
sudo -i
```

* Enter your current user's password.

---

## Become Root with `su`

```bash
su -
```

* Enter the root user's password.

---

## Switch to Another User

```bash
su - username
```

* Enter the target user's password.

---

# Quick Revision

| Command                      | Purpose                                       |
| ---------------------------- | --------------------------------------------- |
| `id`                         | Show UID, GID and groups                      |
| `whoami`                     | Show current username                         |
| `who`                        | Show logged-in users                          |
| `passwd`                     | Change current user's password                |
| `passwd username`            | Change another user's password as root        |
| `sudo`                       | Run a command with root privileges            |
| `sudo -i`                    | Open a root login shell                       |
| `su`                         | Switch user                                   |
| `su -`                       | Switch to root with login environment         |
| `su - username`              | Switch to another user with login environment |
| `sudo passwd username`       | Change another user's password using sudo     |
| `usermod -l`                 | Change username                               |
| `loginctl list-sessions`     | Show active login sessions                    |
| `hostnamectl`                | Show hostname and system information          |
| `hostnamectl set-hostname`   | Change hostname                               |
| `hostname -I`                | Show IP addresses                             |
| `date`                       | Show current date and time                    |
| `date -u`                    | Show UTC date and time                        |
| `date +FORMAT`               | Show custom date and time format              |
| `date -s`                    | Set system date and time                      |
| `timedatectl`                | Show date, time and timezone information      |
| `timedatectl list-timezones` | List available timezones                      |
| `timedatectl set-timezone`   | Change timezone                               |
| `timedatectl set-ntp`        | Enable or disable NTP                         |
| `uptime`                     | Show system uptime                            |
| `uptime -s`                  | Show last boot time                           |

---

## Navigation

[🏠 Back to Home](https://r-lakshman.github.io/Linux-System-Administrator/)
|
[View on GitHub](https://github.com/r-lakshman/Linux-System-Administrator/blob/main/01-linux-basic-commands.md)
|
[Next: Terminal Keyboard Shortcuts →](https://r-lakshman.github.io/Linux-System-Administrator/02-terminal-keyboard-shortcuts.html)

---

© 2026 R Lakshman Kumar. All rights reserved.
