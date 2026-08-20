# Linux Terminal Keyboard Shortcuts

Useful keyboard shortcuts for working with commands in the Linux terminal.

---

## `Ctrl + U` — Delete from Cursor to Beginning

Deletes everything from the cursor to the beginning of the command.

### Before

```text
echo Hello World
         |

Press
Ctrl + U

After
World
|

Ctrl + K — Delete from Cursor to End

Deletes everything from the cursor to the end of the command.

Before
echo Hello World
          |

Press
Ctrl + K

After
echo Hello

Ctrl + W — Delete Previous Word

Deletes the word before the cursor.

Before
echo Hello World
           |

Press
Ctrl + W

After
echo Hello |

Alt + F — Move Forward One Word

Moves the cursor forward by one word.

Before
echo Hello World
     |

Press
Alt + F

After
echo Hello World
          |

Alt + B — Move Backward One Word

Moves the cursor backward by one word.

Before
echo Hello World
          |

Press
Alt + B

After
echo Hello World
     |

Ctrl + A — Move to Beginning

Moves the cursor to the beginning of the command.

Before
echo Hello World
          |

Press
Ctrl + A

After
|echo Hello World

Ctrl + E — Move to End

Moves the cursor to the end of the command.

Before
echo Hello World
     |

Press
Ctrl + E

After
echo Hello World|

Up Arrow (↑) — Previous Command

Shows the previous command from command history.

Before
$

Press
↑

After
$ ls -la


Press ↑ repeatedly to move further back through command history.

Down Arrow (↓) — Next Command

Moves forward through command history.

Before
$ pwd

Press
↓

After
$ cd /tmp

Ctrl + R — Search Command History

Searches previously executed commands.

Before
$

Press
Ctrl + R


Type:

terraform

Example
(reverse-i-search)`terraform': terraform plan


Press Enter to run the command.

Press Ctrl + R again to find older matching commands.

Ctrl + C — Stop / Cancel Command

Stops a currently running command.

Before
$ ping google.com
64 bytes from ...
64 bytes from ...
64 bytes from ...

Press
Ctrl + C

After
^C
$


Commonly used with:

ping google.com
tail -f logfile.txt

Ctrl + Z — Suspend a Command

Temporarily suspends a running process.

Before
$ ping google.com
64 bytes from ...
64 bytes from ...

Press
Ctrl + Z

After
^Z
[1]+  Stopped    ping google.com
$


Check suspended jobs:

jobs


Continue in foreground:

fg


Continue in background:

bg

Ctrl + D — End Input / EOF

Sends an EOF (End Of File) signal.

Example
$ cat
Hello
Linux

Press
Ctrl + D

After
Hello
Linux
$


At an empty shell prompt, Ctrl + D normally exits the shell.

Ctrl + L — Clear Visible Screen

Clears the visible terminal screen.

Before
$ ls
file1.txt
file2.txt

$ pwd
/home/user/linux

$

Press
Ctrl + L

After
$


Ctrl + L does not clear Bash command history.

Previous commands and output can normally still be viewed by scrolling up.

clear — Clear Terminal Display

Clears the terminal display.

Before
$ ls
file1.txt
file2.txt

$ pwd
/home/user/linux

$

Run
clear

After
$


Ctrl + L and clear clear the terminal display.
Neither command clears Bash command history.

To clear Bash command history:

history -c

Ctrl + H — Backspace

Deletes the character before the cursor.

Before
$ echo Hello
           |

Press
Ctrl + H

After
$ echo Hell
          |

Ctrl + Y — Paste Deleted Text

Pastes text previously deleted using commands such as Ctrl + U, Ctrl + K, or Ctrl + W.

Before
$ echo Hello World


After deleting text:

Ctrl + W


Use:

Ctrl + Y

After
$ echo Hello World

Ctrl + _ — Undo

Undoes the previous command-line editing action.

Before
$ echo Hello Wrold

Press
Ctrl + _

After
$ echo Hello World

Ctrl + T — Swap Characters

Swaps characters around the cursor.

Before
$ echo Wrold
       |

Press
Ctrl + T

After
$ echo World

Alt + . — Previous Command's Last Argument

Inserts the last argument from the previous command.

First command
cat /var/log/messages


Now type:

ls


Press:

Alt + .

After
ls /var/log/messages

Quick Reference
Shortcut	Purpose
Ctrl + A	Move to beginning
Ctrl + E	Move to end
Ctrl + U	Delete to beginning
Ctrl + K	Delete to end
Ctrl + W	Delete previous word
Ctrl + H	Backspace
Ctrl + Y	Paste deleted text
Ctrl + _	Undo
Ctrl + T	Swap characters
Alt + B	Move backward one word
Alt + F	Move forward one word
Alt + .	Insert previous command's last argument
↑	Previous command
↓	Next command
Ctrl + R	Search command history
Ctrl + L	Clear visible screen
Ctrl + C	Stop/cancel command
Ctrl + Z	Suspend command
Ctrl + D	End input / EOF
Most Important Shortcuts
Ctrl + A    → Beginning
Ctrl + E    → End

Ctrl + U    → Delete to beginning
Ctrl + K    → Delete to end
Ctrl + W    → Delete previous word

Alt + B     → Backward one word
Alt + F     → Forward one word

↑ / ↓       → Command history
Ctrl + R    → Search command history

Ctrl + L    → Clear screen
Ctrl + C    → Stop command
Ctrl + Z    → Suspend command
Ctrl + D    → End input / EOF

Ctrl + Y    → Paste deleted text
Ctrl + _    → Undo
Alt + .     → Previous command's last argument

