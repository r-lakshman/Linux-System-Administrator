# Linux Basic Commands

A practical reference for commonly used Linux commands for **directory navigation, file management, file viewing, searching, redirection, and command history**.

---

## Table of Contents

1. [Command Syntax](#1-command-syntax)
2. [pwd](#2-pwd--print-working-directory)
3. [ls](#3-ls--list-files-and-directories)
4. [ll](#4-ll--long-listing-alias)
5. [cd](#5-cd--change-directory)
6. [mkdir](#6-mkdir--make-directory)
7. [touch](#7-touch--create-a-file)
8. [cat](#8-cat--display-file-contents)
9. [echo](#9-echo--print-text)
10. [Redirection](#10-redirection)
11. [less](#11-less--view-files)
12. [head](#12-head--show-beginning-of-file)
13. [tail](#13-tail--show-end-of-file)
14. [truncate](#14-truncate--resize-or-empty-file)
15. [grep](#15-grep--search-text)
16. [wc](#16-wc--count-lines-words-and-bytes)
17. [cp](#17-cp--copy)
18. [mv](#18-mv--move-or-rename)
19. [rm](#19-rm--remove)
20. [rmdir](#20-rmdir--remove-empty-directory)
21. [find](#21-find--search-files-and-directories)
22. [history](#22-history--command-history)
23. [Important Path Symbols](#important-path-symbols)
24. [Important Options](#important-linux-options)
25. [Quick Reference](#quick-reference)

---

# 1. Command Syntax

Linux commands generally follow this pattern:

```bash
command [options] [arguments]

Meaning
Part	Meaning
command	The command to execute
[options]	Optional flags that change command behavior
[arguments]	Optional input such as a file, directory, or pattern

[ ] means the item is optional.

Example:

ls [options] [directory]


All of these are valid:

ls
ls -l
ls /home/lakshman
ls -la /home/lakshman

2. pwd — Print Working Directory

Displays the absolute path of the current working directory.

Syntax
pwd

Example
pwd


Output:

/home/lakshman/linux-admin


pwd → Shows where you are currently located.

3. ls — List Files and Directories

Lists files and directories.

Syntax
ls [options] [directory]


Both [options] and [directory] are optional.

If no directory is specified, ls lists the current directory.

Basic Example
ls


Output:

file1.txt
file2.txt
projects

Common Options
Option	Meaning
-a	Show all files, including hidden files
-l	Long/detailed listing
-h	Human-readable sizes
-R	List directories recursively
-d	Show directory itself instead of contents
-t	Sort by modification time
-S	Sort by file size
ls -a — Show Hidden Files

Linux hidden files start with ..

ls -a


Example:

.
..
.bashrc
.config
file.txt
projects


. → Current directory
.. → Parent directory

ls -l — Long Listing
ls -l


Shows information such as:

permissions
owner
group
size
date
file/directory name

ls -la — Detailed + Hidden Files
ls -la

ls -lh — Human-Readable Sizes
ls -lh


Example:

-rw-r--r-- 1 user user 2.5K Aug 20 file.txt

ls -R — Recursive Listing
ls -R


Lists the contents of directories and their subdirectories.

4. ll — Long Listing Alias

ll is commonly configured as an alias for:

ls -l

Syntax
ll [directory]

Example
ll


Check whether ll exists:

alias ll


Output:

alias ll='ls -l'


ll is usually an alias and may not be available on every Linux system.

5. cd — Change Directory

Used to move from one directory to another.

Syntax
cd [directory]

Common Usage
Command	Meaning
cd folder	Enter a directory
cd .	Current directory
cd ..	Parent directory
cd ../folder	Go through parent into another directory
cd ~	Home directory
cd /	Root directory
cd -	Previous working directory
cd	Home directory
cd . — Current Directory

. represents the current directory.

cd .


Example:

$ pwd
/home/lakshman/lk

$ cd .

$ pwd
/home/lakshman/lk


. → Current directory.

cd .. — Parent Directory

.. represents the parent directory.

cd ..


Example:

/home/lakshman/lk
        |
        | cd ..
        v
/home/lakshman


.. → Parent directory, one level above the current directory.

cd ../rlk — Move to Another Directory

Suppose:

/home/lakshman/
├── lk/
├── rlk/
├── lakshman/
└── kumar/


Currently:

/home/lakshman/lk


Go to rlk:

cd ../rlk


Go to kumar:

cd ../kumar


Check your location:

pwd


../rlk → Go to the parent directory, then enter rlk.

cd ~ — Home Directory
cd ~


Moves to the user's home directory.

cd / — Root Directory
cd /


Moves to the root directory.

cd - — Previous Directory
cd -


Moves to the previous working directory.

6. mkdir — Make Directory

Creates directories.

Syntax
mkdir [options] directory_name

Common Options
Option	Meaning
-p	Create parent directories
-v	Show what is being created
-m	Set directory permissions
Create One Directory
mkdir projects

Create Multiple Directories
mkdir folder1 folder2 folder3

Brace Expansion
mkdir folder{1..3}


Creates:

folder1
folder2
folder3

Directory Names with Spaces
mkdir "folder "{1..3}


Creates:

folder 1
folder 2
folder 3

mkdir -p
mkdir -p parent/child/grandchild


Creates the complete directory structure.

mkdir → Make Directory.

7. touch — Create a File

Creates an empty file or updates file timestamps.

Syntax
touch [options] file_name

Common Options
Option	Meaning
-a	Change access time
-m	Change modification time
-c	Do not create file if it does not exist
-d	Use specified date/time
Create One File
touch file.txt

Create Multiple Files
touch file1.txt file2.txt file3.txt

Create 10 Files
touch file{1..10}


Creates:

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

Create Files with Spaces
touch "file "{1..10}


Creates:

file 1
file 2
file 3
...
file 10

8. cat — Display File Contents

Displays the contents of a file.

Syntax
cat [options] file

Common Options
Option	Meaning
-n	Number all lines
-b	Number non-empty lines
-s	Remove repeated blank lines
-E	Show $ at end of lines
-T	Show TAB characters
Display File
cat file.txt

Show Line Numbers
cat -n file.txt

Copy Contents
cat file1.txt > file2.txt


> overwrites file2.txt.

Append Contents
cat file1.txt >> file2.txt


>> appends to file2.txt.

9. echo — Print Text

Prints text or variable values.

Syntax
echo [options] [text]

Common Options
Option	Meaning
-n	Do not print a new line
-e	Enable escape sequences
-E	Disable escape sequences
Example
echo "Hello, World!"


Output:

Hello, World!

echo -e
echo -e "Hello\nWorld"


Output:

Hello
World


-e → Enables interpretation of escape sequences.

Common Escape Characters
Escape	Meaning
\n	New line
\t	Tab space
\\	Print backslash
\a	Alert sound
\b	Backspace
10. Redirection

Linux provides operators to redirect command output.

> — Overwrite
Syntax
command > file


Example:

echo "Linux" > file.txt


If file.txt already contains:

Hello
World


After the command:

Linux


> creates the file if it does not exist and overwrites it if it exists.

>> — Append
Syntax
command >> file


Example:

echo "DevOps" >> file.txt


If the file contains:

Linux


After:

Linux
DevOps


>> adds content to the end without overwriting existing content.

11. less — View Files

Views a file one screen at a time.

Syntax
less [options] file

Common Options
Option	Meaning
-N	Show line numbers
-S	Do not wrap long lines
-i	Ignore case during search
-F	Exit if the file fits on one screen
Examples
less file.txt
less -N file.txt
less -S file.txt

Useful Keys
Key	Meaning
Space	Next page
b	Previous page
↑	Move up
↓	Move down
/text	Search
n	Next match
N	Previous match
q	Quit
12. head — Show Beginning of File

Shows the first 10 lines by default.

Syntax
head [options] file

Common Options
Option	Meaning
-n	Number of lines
-c	Number of bytes
-q	Hide file headers
-v	Show file headers
Examples

First 10 lines:

head file.txt


First 5 lines:

head -5 file.txt


or:

head -n 5 file.txt


First 50 lines:

head -50 file.txt

13. tail — Show End of File

Shows the last 10 lines by default.

Syntax
tail [options] file

Common Options
Option	Meaning
-n	Number of lines
-c	Number of bytes
-f	Follow file changes
-F	Follow file even if recreated
-q	Hide file headers
-v	Show file headers
Examples

Last 10 lines:

tail file.txt


Last 5 lines:

tail -5 file.txt


Last 50 lines:

tail -50 file.txt

Follow Log File
tail -f logfile.txt


Stop with:

Ctrl + C

14. truncate — Resize or Empty a File

Changes the size of a file.

Syntax
truncate [options] file

Common Options
Option	Meaning
-s	Set file size
-c	Do not create file if it does not exist
Empty a File
truncate -s 0 file.txt


-s 0 → Set the file size to zero bytes.

Set File Size
truncate -s 5 file.txt


Sets the file size to 5 bytes.

15. grep — Search Text

Searches for matching text in files.

Syntax
grep [options] pattern file

Common Options
Option	Meaning
-i	Ignore case
-n	Show line numbers
-o	Show only matching text
-v	Show non-matching lines
-c	Count matching lines
-r	Search recursively
-R	Recursive search including symbolic links
-w	Match whole words
-x	Match whole lines
-l	Show file names with matches
-L	Show files without matches
-h	Hide file names
-H	Show file names
Examples

Basic search:

grep "Lakshman" file.txt


Ignore case:

grep -i "lakshman" file.txt


Show line number:

grep -n "Lakshman" file.txt


Show only matching word:

grep -o "Lakshman" file.txt


Show lines that do NOT match:

grep -v "Lakshman" file.txt


Count matching lines:

grep -c "Lakshman" file.txt


Search recursively:

grep -r "Lakshman" /home/lakshman/


Combine options:

grep -o -i -n "text" file.txt


grep -v → Shows lines that do not contain the pattern.

16. wc — Count Lines, Words and Bytes
Syntax
wc [options] file

Common Options
Option	Meaning
-l	Count lines
-w	Count words
-c	Count bytes
-m	Count characters
Examples
wc file.txt
wc -l file.txt
wc -w file.txt
wc -c file.txt
wc -m file.txt

17. cp — Copy Files and Directories

Copies files and directories.

Syntax
cp [options] source destination

Common Options
Option	Meaning
-r	Copy directories recursively
-R	Copy recursively
-a	Archive; preserve attributes and copy recursively
-i	Ask before overwrite
-f	Force overwrite
-v	Show what is being copied
-p	Preserve permissions and timestamps
-u	Copy if source is newer or destination is missing
Copy File
cp file.txt backup.txt

Copy File to Directory
cp file.txt /home/user/Documents/

Copy Directory
cp -r source_folder destination_folder

Archive Copy
cp -a source_folder destination_folder

Interactive Copy
cp -i file.txt backup.txt

Verbose Copy
cp -v file.txt backup.txt


cp → Copy source → destination.

18. mv — Move or Rename

Moves or renames files and directories.

Syntax
mv [options] source destination

Common Options
Option	Meaning
-i	Ask before overwrite
-f	Force overwrite
-v	Show what is being moved
-n	Do not overwrite existing destination
-u	Move if source is newer
Rename File
mv old.txt new.txt

Move File
mv file.txt /home/user/Documents/

Move Directory
mv folder1 /tmp/

Interactive
mv -i file.txt /tmp/

Verbose
mv -v file.txt /tmp/


mv → Move or rename source → destination.

19. rm — Remove Files and Directories

Removes files and directories.

Syntax
rm [options] file_or_directory

Common Options
Option	Meaning
-r	Remove recursively
-R	Remove recursively
-f	Force removal
-i	Ask before removal
-I	Ask once before removing many files
-v	Show what is being removed
Remove File
rm file.txt

Remove Multiple Files
rm file1.txt file2.txt

Remove Directory
rm -r folder

Force Remove Directory
rm -rf folder


-r → Recursive
-f → Force
-rf → Recursive + Force

Interactive Remove
rm -i file.txt

Verbose Remove
rm -v file.txt

Remove Everything Inside a Directory
rm -rf /tmp/user/home/Lucky/*


Here:

.. → Parent directory
*  → Everything matched inside the directory


Warning: rm -rf can permanently delete data. Use it carefully.

20. rmdir — Remove Empty Directory

Removes an empty directory.

Syntax
rmdir [options] directory

Common Options
Option	Meaning
-p	Remove parent directories if empty
-v	Show what is being removed
Example
rmdir projects


For nested empty directories:

rmdir -p parent/child


rmdir only removes empty directories.

21. find — Search Files and Directories

Searches for files and directories.

Syntax
find [path] [options] [expression]

Common Options
Option	Meaning
-name	Search by name
-iname	Search by name, ignoring case
-type f	Find files
-type d	Find directories
-size	Search by size
-mtime	Search by modification time
-user	Search by owner
-perm	Search by permissions
-maxdepth	Limit search depth
-exec	Execute command on results
Find a File
find . -name "file.txt"

Find .log Files
find . -name "*.log"

Find Files
find . -type f

Find Directories
find . -type d

Case-Insensitive Search
find . -iname "file.txt"

Limit Search Depth
find . -maxdepth 2 -name "*.txt"

22. history — Command History

Displays previously executed commands.

Syntax
history [number]

Show History
history

Show Last 10 Commands
history 10

Search History
history | grep terraform

Run a Command by History Number

First:

history


Example:

103  cat file.txt
104  pwd
105  ls -la


Run command 103:

!103


This executes:

cat file.txt

Run Previous Command
!!

Clear History
history -c

Important Linux Path Symbols
Symbol	Meaning	Example
.	Current directory	cd .
..	Parent directory	cd ..
~	Home directory	cd ~
/	Root directory	cd /
*	Wildcard	rm *.txt
Important Linux Options

These are common meanings, but the exact meaning depends on the command.

Option	Common Meaning
-a	All / hidden files / archive
-l	Long or detailed listing
-h	Human-readable
-r	Recursive
-R	Recursive
-f	Force
-i	Interactive / ignore case depending on command
-v	Verbose
-n	Number / no newline depending on command
-p	Parent / preserve depending on command
-c	Count / bytes depending on command
-o	Output only matching text / command-specific
-d	Directory / date / command-specific

Important: Options are command-specific. For example:

grep -i → Ignore case
rm -i → Ask for confirmation
echo -i → Not a standard option

To check available options:

command --help


Examples:

ls --help
cp --help
rm --help
grep --help

Redirection and Pipe Operators
Operator	Meaning	Example
>	Overwrite output	echo "Linux" > file.txt
>>	Append output	echo "Linux" >> file.txt
`	`	Pipe output to another command
Common Command Patterns
File Copy
cp [options] source destination


Example:

cp file.txt backup.txt

File Move / Rename
mv [options] source destination


Example:

mv old.txt new.txt

File Removal
rm [options] file


Example:

rm -f file.txt

Directory Removal
rm -r directory


Force recursive removal:

rm -rf directory

Text Search
grep [options] pattern file


Example:

grep -in "error" logfile.txt

Directory Search
find [path] [options] [expression]


Example:

find /var/log -name "*.log"

Practical Command Flow
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

Quick Reference
Command	Syntax	Purpose
pwd	pwd	Show current directory
ls	ls [options] [directory]	List files/directories
ll	ll [directory]	Common alias for ls -l
cd	cd [directory]	Change directory
mkdir	mkdir [options] directory	Create directory
touch	touch [options] file	Create file
cat	cat [options] file	Display file
echo	echo [options] text	Print text
less	less [options] file	View file
head	head [options] file	Show beginning
tail	tail [options] file	Show end
truncate	truncate [options] file	Resize/empty file
grep	grep [options] pattern file	Search text
wc	wc [options] file	Count lines/words/bytes
cp	cp [options] source destination	Copy
mv	mv [options] source destination	Move/rename
rm	rm [options] file	Remove
rmdir	rmdir [options] directory	Remove empty directory
find	find [path] [options] [expression]	Search
history	history [number]	Show command history
Key Points to Remember
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


Best practice: Do not memorize every option. Learn the common options and use command --help whenever you need to verify an option.

## Copyright

© 2026 R Lakshma Kumar. All rights reserved.
