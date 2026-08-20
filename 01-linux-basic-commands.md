# Linux Basic Commands

A practical reference for commonly used Linux commands for **directory navigation, file management, file viewing, searching, redirection, and command history**.

---

## Table of Contents

1. [Command Syntax](#1-command-syntax)
2. [pwd — Print Working Directory](#2-pwd--print-working-directory)
3. [ls — List Files and Directories](#3-ls--list-files-and-directories)
4. [ll — Long Listing Alias](#4-ll--long-listing-alias)
5. [cd — Change Directory](#5-cd--change-directory)
6. [mkdir — Make Directory](#6-mkdir--make-directory)
7. [touch — Create a File](#7-touch--create-a-file)
8. [cat — Display File Contents](#8-cat--display-file-contents)
9. [echo — Print Text](#9-echo--print-text)
10. [Redirection](#10-redirection)
11. [less — View Files](#11-less--view-files)
12. [head — Show Beginning of File](#12-head--show-beginning-of-file)
13. [tail — Show End of File](#13-tail--show-end-of-file)
14. [truncate — Resize or Empty File](#14-truncate--resize-or-empty-file)
15. [grep — Search Text](#15-grep--search-text)
16. [wc — Count Lines, Words and Bytes](#16-wc--count-lines-words-and-bytes)
17. [cp — Copy](#17-cp--copy)
18. [mv — Move or Rename](#18-mv--move-or-rename)
19. [rm — Remove](#19-rm--remove)
20. [rmdir — Remove Empty Directory](#20-rmdir--remove-empty-directory)
21. [find — Search Files and Directories](#21-find--search-files-and-directories)
22. [history — Command History](#22-history--command-history)
23. [Important Path Symbols](#23-important-path-symbols)
24. [Important Linux Options](#24-important-linux-options)
25. [Redirection and Pipe Operators](#25-redirection-and-pipe-operators)
26. [Common Command Patterns](#26-common-command-patterns)
27. [Practical Command Flow](#27-practical-command-flow)
28. [Quick Reference](#28-quick-reference)
29. [Key Points to Remember](#29-key-points-to-remember)

---

# 1. Command Syntax

Linux commands generally follow this pattern:

```bash
command [options] [arguments]
```

### Meaning

| Part          | Meaning                                              |
| ------------- | ---------------------------------------------------- |
| `command`     | The command to execute                               |
| `[options]`   | Optional flags that change command behavior          |
| `[arguments]` | Optional input such as a file, directory, or pattern |

`[ ]` means the item is optional.

### Example

```bash
ls [options] [directory]
```

All of these are valid:

```bash
ls
ls -l
ls /home/lakshman
ls -la /home/lakshman
```

---

# 2. pwd — Print Working Directory

Displays the absolute path of the current working directory.

## Syntax

```bash
pwd
```

## Example

```bash
pwd
```

Output:

```text
/home/lakshman/linux-admin
```

`pwd` → Shows where you are currently located.

---

# 3. ls — List Files and Directories

Lists files and directories.

## Syntax

```bash
ls [options] [directory]
```

Both `[options]` and `[directory]` are optional.

If no directory is specified, `ls` lists the current directory.

## Basic Example

```bash
ls
```

Example output:

```text
file1.txt
file2.txt
projects
```

## Common Options

| Option | Meaning                                   |
| ------ | ----------------------------------------- |
| `-a`   | Show all files, including hidden files    |
| `-l`   | Long/detailed listing                     |
| `-h`   | Human-readable sizes                      |
| `-R`   | List directories recursively              |
| `-d`   | Show directory itself instead of contents |
| `-t`   | Sort by modification time                 |
| `-S`   | Sort by file size                         |

## ls -a — Show Hidden Files

Linux hidden files start with `.`.

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

* `.` → Current directory
* `..` → Parent directory

## ls -l — Long Listing

```bash
ls -l
```

Shows information such as:

* Permissions
* Owner
* Group
* Size
* Date
* File/directory name

## ls -la — Detailed + Hidden Files

```bash
ls -la
```

## ls -lh — Human-Readable Sizes

```bash
ls -lh
```

Example:

```text
-rw-r--r-- 1 user user 2.5K Aug 20 file.txt
```

## ls -R — Recursive Listing

```bash
ls -R
```

Lists the contents of directories and their subdirectories.

---

# 4. ll — Long Listing Alias

`ll` is commonly configured as an alias for:

```bash
ls -l
```

## Syntax

```bash
ll [directory]
```

## Example

```bash
ll
```

Check whether `ll` exists:

```bash
alias ll
```

Example output:

```text
alias ll='ls -l'
```

> `ll` is usually an alias and may not be available on every Linux system.

---

# 5. cd — Change Directory

Used to move from one directory to another.

## Syntax

```bash
cd [directory]
```

## Common Usage

| Command        | Meaning                                  |
| -------------- | ---------------------------------------- |
| `cd folder`    | Enter a directory                        |
| `cd .`         | Current directory                        |
| `cd ..`        | Parent directory                         |
| `cd ../folder` | Go through parent into another directory |
| `cd ~`         | Home directory                           |
| `cd /`         | Root directory                           |
| `cd -`         | Previous working directory               |

## cd . — Current Directory

`.` represents the current directory.

```bash
cd .
```

Example:

```text
$ pwd
/home/lakshman/lk

$ cd .

$ pwd
/home/lakshman/lk
```

`.` → Current directory.

## cd .. — Parent Directory

`..` represents the parent directory.

```bash
cd ..
```

Example:

```text
/home/lakshman/lk
       |
       | cd ..
       v
/home/lakshman
```

`..` → Parent directory, one level above the current directory.

## cd ../rlk — Move to Another Directory

Suppose:

```text
/home/lakshman/
├── lk/
├── rlk/
├── lakshman/
└── kumar/
```

Currently:

```text
/home/lakshman/lk
```

Go to `rlk`:

```bash
cd ../rlk
```

Go to `kumar`:

```bash
cd ../kumar
```

Check your location:

```bash
pwd
```

`../rlk` → Go to the parent directory, then enter `rlk`.

## cd ~ — Home Directory

```bash
cd ~
```

Moves to the user's home directory.

## cd / — Root Directory

```bash
cd /
```

Moves to the root directory.

## cd - — Previous Directory

```bash
cd -
```

Moves to the previous working directory.

---

# 6. mkdir — Make Directory

Creates directories.

## Syntax

```bash
mkdir [options] directory_name
```

## Common Options

| Option | Meaning                    |
| ------ | -------------------------- |
| `-p`   | Create parent directories  |
| `-v`   | Show what is being created |
| `-m`   | Set directory permissions  |

## Create One Directory

```bash
mkdir projects
```

## Create Multiple Directories

```bash
mkdir folder1 folder2 folder3
```

## Brace Expansion

```bash
mkdir folder{1..3}
```

Creates:

```text
folder1
folder2
folder3
```

## Directory Names with Spaces

```bash
mkdir "folder "{1..3}
```

Creates:

```text
folder 1
folder 2
folder 3
```

## mkdir -p

```bash
mkdir -p parent/child/grandchild
```

Creates the complete directory structure.

`mkdir` → Make Directory.

---

# 7. touch — Create a File

Creates an empty file or updates file timestamps.

## Syntax

```bash
touch [options] file_name
```

## Common Options

| Option | Meaning                                 |
| ------ | --------------------------------------- |
| `-a`   | Change access time                      |
| `-m`   | Change modification time                |
| `-c`   | Do not create file if it does not exist |
| `-d`   | Use specified date/time                 |

## Create One File

```bash
touch file.txt
```

## Create Multiple Files

```bash
touch file1.txt file2.txt file3.txt
```

## Create 10 Files

```bash
touch file{1..10}
```

Creates:

```text
file1
file2
file3
file4
file5
file6
file7
file8
file9
file10
```

## Create Files with Spaces

```bash
touch "file "{1..10}
```

Creates:

```text
file 1
file 2
file 3
...
file 10
```

---

# 8. cat — Display File Contents

Displays the contents of a file.

## Syntax

```bash
cat [options] file
```

## Common Options

| Option | Meaning                     |
| ------ | --------------------------- |
| `-n`   | Number all lines            |
| `-b`   | Number non-empty lines      |
| `-s`   | Remove repeated blank lines |
| `-E`   | Show `$` at end of lines    |
| `-T`   | Show TAB characters         |

## Display File

```bash
cat file.txt
```

## Show Line Numbers

```bash
cat -n file.txt
```

## Copy Contents

```bash
cat file1.txt > file2.txt
```

`>` overwrites `file2.txt`.

## Append Contents

```bash
cat file1.txt >> file2.txt
```

`>>` appends to `file2.txt`.

---

# 9. echo — Print Text

Prints text or variable values.

## Syntax

```bash
echo [options] [text]
```

## Common Options

| Option | Meaning                  |
| ------ | ------------------------ |
| `-n`   | Do not print a new line  |
| `-e`   | Enable escape sequences  |
| `-E`   | Disable escape sequences |

## Example

```bash
echo "Hello, World!"
```

Output:

```text
Hello, World!
```

## echo -e

```bash
echo -e "Hello\nWorld"
```

Output:

```text
Hello
World
```

`-e` → Enables interpretation of escape sequences.

## Common Escape Characters

| Escape | Meaning         |
| ------ | --------------- |
| `\n`   | New line        |
| `\t`   | Tab space       |
| `\\`   | Print backslash |
| `\a`   | Alert sound     |
| `\b`   | Backspace       |

---

# 10. Redirection

Linux provides operators to redirect command output.

## > — Overwrite

### Syntax

```bash
command > file
```

Example:

```bash
echo "Linux" > file.txt
```

If `file.txt` already contains:

```text
Hello World
```

After the command:

```text
Linux
```

`>` creates the file if it does not exist and overwrites it if it exists.

## >> — Append

### Syntax

```bash
command >> file
```

Example:

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

`>>` adds content to the end without overwriting existing content.

---

# 11. less — View Files

Views a file one screen at a time.

## Syntax

```bash
less [options] file
```

## Common Options

| Option | Meaning                             |
| ------ | ----------------------------------- |
| `-N`   | Show line numbers                   |
| `-S`   | Do not wrap long lines              |
| `-i`   | Ignore case during search           |
| `-F`   | Exit if the file fits on one screen |

## Examples

```bash
less file.txt
```

```bash
less -N file.txt
```

```bash
less -S file.txt
```

## Useful Keys

| Key     | Meaning        |
| ------- | -------------- |
| `Space` | Next page      |
| `b`     | Previous page  |
| `↑`     | Move up        |
| `↓`     | Move down      |
| `/text` | Search         |
| `n`     | Next match     |
| `N`     | Previous match |
| `q`     | Quit           |

---

# 12. head — Show Beginning of File

Shows the first 10 lines by default.

## Syntax

```bash
head [options] file
```

## Common Options

| Option | Meaning           |
| ------ | ----------------- |
| `-n`   | Number of lines   |
| `-c`   | Number of bytes   |
| `-q`   | Hide file headers |
| `-v`   | Show file headers |

## Examples

First 10 lines:

```bash
head file.txt
```

First 5 lines:

```bash
head -5 file.txt
```

or:

```bash
head -n 5 file.txt
```

First 50 lines:

```bash
head -50 file.txt
```

---

# 13. tail — Show End of File

Shows the last 10 lines by default.

## Syntax

```bash
tail [options] file
```

## Common Options

| Option | Meaning                       |
| ------ | ----------------------------- |
| `-n`   | Number of lines               |
| `-c`   | Number of bytes               |
| `-f`   | Follow file changes           |
| `-F`   | Follow file even if recreated |
| `-q`   | Hide file headers             |
| `-v`   | Show file headers             |

## Examples

Last 10 lines:

```bash
tail file.txt
```

Last 5 lines:

```bash
tail -5 file.txt
```

Last 50 lines:

```bash
tail -50 file.txt
```

## Follow Log File

```bash
tail -f logfile.txt
```

Stop with:

```text
Ctrl + C
```

---

# 14. truncate — Resize or Empty File

Changes the size of a file.

## Syntax

```bash
truncate [options] file
```

## Common Options

| Option | Meaning                                 |
| ------ | --------------------------------------- |
| `-s`   | Set file size                           |
| `-c`   | Do not create file if it does not exist |

## Empty a File

```bash
truncate -s 0 file.txt
```

`-s 0` → Set the file size to zero bytes.

## Set File Size

```bash
truncate -s 5 file.txt
```

Sets the file size to 5 bytes.

---

# 15. grep — Search Text

Searches for matching text in files.

## Syntax

```bash
grep [options] pattern file
```

## Common Options

| Option | Meaning                                   |
| ------ | ----------------------------------------- |
| `-i`   | Ignore case                               |
| `-n`   | Show line numbers                         |
| `-o`   | Show only matching text                   |
| `-v`   | Show non-matching lines                   |
| `-c`   | Count matching lines                      |
| `-r`   | Search recursively                        |
| `-R`   | Recursive search including symbolic links |
| `-w`   | Match whole words                         |
| `-x`   | Match whole lines                         |
| `-l`   | Show file names with matches              |
| `-L`   | Show files without matches                |
| `-h`   | Hide file names                           |
| `-H`   | Show file names                           |

## Basic Search

```bash
grep "Lakshman" file.txt
```

## Ignore Case

```bash
grep -i "lakshman" file.txt
```

## Show Line Number

```bash
grep -n "Lakshman" file.txt
```

## Show Only Matching Text

```bash
grep -o "Lakshman" file.txt
```

## Show Lines That Do NOT Match

```bash
grep -v "Lakshman" file.txt
```

## Count Matching Lines

```bash
grep -c "Lakshman" file.txt
```

## Search Recursively

```bash
grep -r "Lakshman" /home/lakshman/
```

## Combine Options

```bash
grep -o -i -n "text" file.txt
```

`grep -v` → Shows lines that do not contain the pattern.

---

# 16. wc — Count Lines, Words and Bytes

## Syntax

```bash
wc [options] file
```

## Common Options

| Option | Meaning          |
| ------ | ---------------- |
| `-l`   | Count lines      |
| `-w`   | Count words      |
| `-c`   | Count bytes      |
| `-m`   | Count characters |

## Examples

```bash
wc file.txt
```

```bash
wc -l file.txt
```

```bash
wc -w file.txt
```

```bash
wc -c file.txt
```

```bash
wc -m file.txt
```

---

# 17. cp — Copy Files and Directories

Copies files and directories.

## Syntax

```bash
cp [options] source destination
```

## Common Options

| Option | Meaning                                           |
| ------ | ------------------------------------------------- |
| `-r`   | Copy directories recursively                      |
| `-R`   | Copy recursively                                  |
| `-a`   | Archive; preserve attributes and copy recursively |
| `-i`   | Ask before overwrite                              |
| `-f`   | Force overwrite                                   |
| `-v`   | Show what is being copied                         |
| `-p`   | Preserve permissions and timestamps               |
| `-u`   | Copy if source is newer or destination is missing |

## Copy File

```bash
cp file.txt backup.txt
```

## Copy File to Directory

```bash
cp file.txt /home/user/Documents/
```

## Copy Directory

```bash
cp -r source_folder destination_folder
```

## Archive Copy

```bash
cp -a source_folder destination_folder
```

## Interactive Copy

```bash
cp -i file.txt backup.txt
```

## Verbose Copy

```bash
cp -v file.txt backup.txt
```

`cp` → Copy source → destination.

---

# 18. mv — Move or Rename

Moves or renames files and directories.

## Syntax

```bash
mv [options] source destination
```

## Common Options

| Option | Meaning                               |
| ------ | ------------------------------------- |
| `-i`   | Ask before overwrite                  |
| `-f`   | Force overwrite                       |
| `-v`   | Show what is being moved              |
| `-n`   | Do not overwrite existing destination |
| `-u`   | Move if source is newer               |

## Rename File

```bash
mv old.txt new.txt
```

## Move File

```bash
mv file.txt /home/user/Documents/
```

## Move Directory

```bash
mv folder1 /tmp/
```

## Interactive

```bash
mv -i file.txt /tmp/
```

## Verbose

```bash
mv -v file.txt /tmp/
```

`mv` → Move or rename source → destination.

---

# 19. rm — Remove Files and Directories

Removes files and directories.

## Syntax

```bash
rm [options] file_or_directory
```

## Common Options

| Option | Meaning                             |
| ------ | ----------------------------------- |
| `-r`   | Remove recursively                  |
| `-R`   | Remove recursively                  |
| `-f`   | Force removal                       |
| `-i`   | Ask before removal                  |
| `-I`   | Ask once before removing many files |
| `-v`   | Show what is being removed          |

## Remove File

```bash
rm file.txt
```

## Remove Multiple Files

```bash
rm file1.txt file2.txt
```

## Remove Directory

```bash
rm -r folder
```

## Force Remove Directory

```bash
rm -rf folder
```

* `-r` → Recursive
* `-f` → Force
* `-rf` → Recursive + Force

## Interactive Remove

```bash
rm -i file.txt
```

## Verbose Remove

```bash
rm -v file.txt
```

## Remove Everything Inside a Directory

```bash
rm -rf /tmp/user/home/Lucky/*
```

Here:

* `..` → Parent directory
* `*` → Everything matched inside the directory

> **Warning:** `rm -rf` can permanently delete data. Use it carefully.

---

# 20. rmdir — Remove Empty Directory

Removes an empty directory.

## Syntax

```bash
rmdir [options] directory
```

## Common Options

| Option | Meaning                            |
| ------ | ---------------------------------- |
| `-p`   | Remove parent directories if empty |
| `-v`   | Show what is being removed         |

## Example

```bash
rmdir projects
```

For nested empty directories:

```bash
rmdir -p parent/child
```

`rmdir` only removes empty directories.

---

# 21. find — Search Files and Directories

Searches for files and directories.

## Syntax

```bash
find [path] [options] [expression]
```

## Common Options

| Option      | Meaning                       |
| ----------- | ----------------------------- |
| `-name`     | Search by name                |
| `-iname`    | Search by name, ignoring case |
| `-type f`   | Find files                    |
| `-type d`   | Find directories              |
| `-size`     | Search by size                |
| `-mtime`    | Search by modification time   |
| `-user`     | Search by owner               |
| `-perm`     | Search by permissions         |
| `-maxdepth` | Limit search depth            |
| `-exec`     | Execute command on results    |

## Find a File

```bash
find . -name "file.txt"
```

## Find .log Files

```bash
find . -name "*.log"
```

## Find Files

```bash
find . -type f
```

## Find Directories

```bash
find . -type d
```

## Case-Insensitive Search

```bash
find . -iname "file.txt"
```

## Limit Search Depth

```bash
find . -maxdepth 2 -name "*.txt"
```

---

# 22. history — Command History

Displays previously executed commands.

## Syntax

```bash
history [number]
```

## Show History

```bash
history
```

## Show Last 10 Commands

```bash
history 10
```

## Search History

```bash
history | grep terraform
```

## Run a Command by History Number

First:

```bash
history
```

Example:

```text
103  cat file.txt
104  pwd
105  ls -la
```

Run command `103`:

```bash
!103
```

This executes:

```bash
cat file.txt
```

## Run Previous Command

```bash
!!
```

## Clear History

```bash
history -c
```

---

# 23. Important Path Symbols

| Symbol | Meaning           | Example    |
| ------ | ----------------- | ---------- |
| `.`    | Current directory | `cd .`     |
| `..`   | Parent directory  | `cd ..`    |
| `~`    | Home directory    | `cd ~`     |
| `/`    | Root directory    | `cd /`     |
| `*`    | Wildcard          | `rm *.txt` |

---

# 24. Important Linux Options

These are common meanings, but the exact meaning depends on the command.

| Option | Common Meaning                                 |
| ------ | ---------------------------------------------- |
| `-a`   | All / hidden files / archive                   |
| `-l`   | Long or detailed listing                       |
| `-h`   | Human-readable                                 |
| `-r`   | Recursive                                      |
| `-R`   | Recursive                                      |
| `-f`   | Force                                          |
| `-i`   | Interactive / ignore case depending on command |
| `-v`   | Verbose                                        |
| `-n`   | Number / no newline depending on command       |
| `-p`   | Parent / preserve depending on command         |
| `-c`   | Count / bytes depending on command             |
| `-o`   | Output only matching text / command-specific   |
| `-d`   | Directory / date / command-specific            |

> **Important:** Options are command-specific.

For example:

```bash
grep -i
```

→ Ignore case

```bash
rm -i
```

→ Ask for confirmation

```bash
echo -i
```

→ Not a standard option

To check available options:

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

# 25. Redirection and Pipe Operators

| Operator | Meaning                        | Example                    |
| -------- | ------------------------------ | -------------------------- |
| `>`      | Overwrite output               | `echo "Linux" > file.txt`  |
| `>>`     | Append output                  | `echo "Linux" >> file.txt` |
| `\|`     | Pipe output to another command | `ls -l \| grep txt`        |

## Pipe Example

```bash
ls -l | grep ".txt"
```

The output of `ls -l` is passed as input to `grep`.

---

# 26. Common Command Patterns

## File Copy

```bash
cp [options] source destination
```

Example:

```bash
cp file.txt backup.txt
```

## File Move / Rename

```bash
mv [options] source destination
```

Example:

```bash
mv old.txt new.txt
```

## File Removal

```bash
rm [options] file
```

Example:

```bash
rm -f file.txt
```

## Directory Removal

```bash
rm -r directory
```

Force recursive removal:

```bash
rm -rf directory
```

## Text Search

```bash
grep [options] pattern file
```

Example:

```bash
grep -in "error" logfile.txt
```

## Directory Search

```bash
find [path] [options] [expression]
```

Example:

```bash
find /var/log -name "*.log"
```

---

# 27. Practical Command Flow

```bash
# Check current location
pwd

# List files
ls

# List detailed files
ls -l

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

# Go back to parent directory
cd ..

# Check location
pwd
```

---

# 28. Quick Reference

| Command    | Syntax                               | Purpose                  |
| ---------- | ------------------------------------ | ------------------------ |
| `pwd`      | `pwd`                                | Show current directory   |
| `ls`       | `ls [options] [directory]`           | List files/directories   |
| `ll`       | `ll [directory]`                     | Common alias for `ls -l` |
| `cd`       | `cd [directory]`                     | Change directory         |
| `mkdir`    | `mkdir [options] directory`          | Create directory         |
| `touch`    | `touch [options] file`               | Create file              |
| `cat`      | `cat [options] file`                 | Display file             |
| `echo`     | `echo [options] text`                | Print text               |
| `less`     | `less [options] file`                | View file                |
| `head`     | `head [options] file`                | Show beginning           |
| `tail`     | `tail [options] file`                | Show end                 |
| `truncate` | `truncate [options] file`            | Resize/empty file        |
| `grep`     | `grep [options] pattern file`        | Search text              |
| `wc`       | `wc [options] file`                  | Count lines/words/bytes  |
| `cp`       | `cp [options] source destination`    | Copy                     |
| `mv`       | `mv [options] source destination`    | Move/rename              |
| `rm`       | `rm [options] file`                  | Remove                   |
| `rmdir`    | `rmdir [options] directory`          | Remove empty directory   |
| `find`     | `find [path] [options] [expression]` | Search files/directories |
| `history`  | `history [number]`                   | Show command history     |

---

# 29. Key Points to Remember

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

## Best Practice

Do not memorize every option.

Learn the common options and use `--help` whenever you need to verify an option.

```bash
command --help
```

Examples:

```bash
ls --help
cp --help
mv --help
rm --help
grep --help
find --help
```

---

© 2026 R Lakshma Kumar. All rights reserved.

