# Linux System Administrator

Linux system administration notes, commands, shortcuts, and practical guides.

---

[← Back to README](https://r-lakshman.github.io/Linux-System-Administrator/)

---

# Linux File Navigation and Editing Using `vi` Editor

> **Important:** Whenever you are in **Insert/Edit Mode** and want to use a Normal Mode command, press **`Esc` first** to return to Normal Mode.

---

## 1. Opening a File with `vi`

**Mode: Linux Terminal**

- To open a file with `vi`:

  ```bash
  vi filename
````

* Example:

  ```bash
  vi test.txt
  ```

* When `vi` opens, it starts in **Normal/Command Mode**.

* Press `i` to enter **Insert/Edit Mode**.

> **Note:** Press **`Esc`** to return from Insert/Edit Mode to Normal/Command Mode.

---

## 2. Normal Mode

**Mode: Normal/Command Mode**

> **Note:** If you are in Insert Mode, press **`Esc`** first.

* `Esc` → Return to Normal Mode.
* `Ctrl + D` → Scroll down.
* `Ctrl + U` → Scroll up.

### Navigation

* `0` → Beginning of the current line.
* `$` → End of the current line.
* `gg` → Go to the first line of the file.
* `G` → Go to the last line of the file.
* `G$` → Go to the last line and move to the end of that line.

---

## 3. Insert/Edit Mode

**Mode: Insert/Edit Mode**

* `i` → Insert before the cursor.
* `a` → Insert after the cursor.
* `o` → Create a new line below the current line.
* `O` → Create a new line above the current line.

### Insert Mode Shortcuts

* `Ctrl + U` → Delete/remove text backward.
* `Ctrl + W` → Delete the previous word.

> **Note:** There is no direct forward-delete shortcut for these actions in Insert Mode. Press **`Esc`** to return to Normal Mode and use the delete commands.

### Forward Deletion

**Mode: Normal Mode**

> **Note:** Press **`Esc`** first to return from Insert Mode.

* `Esc + x` → Delete the character under the cursor.
* `Esc + dw` → Delete forward by word.
* `Esc + D` → Delete forward to the end of the line.
* `Esc + db` → Delete backward to the previous word.

---

## 4. Command-Line Mode

**Mode: Command-Line Mode**

> **Note:** Press **`Esc`** first to return to Normal Mode, then press **`:`**.

* `:wq` → Save the file and exit `vi`.
* `:q!` → Exit without saving changes.
* `:qa!` → Quit all open files without saving changes.
* `:w` → Save the file without quitting.
* `:w filename` → Save the file with a different filename without quitting.

---

## 5. Delete Commands

**Mode: Normal Mode**

> **Note:** Press **`Esc`** first if you are in Insert Mode.

* `Esc + db` → Delete backward to the beginning of the previous word.
* `Esc + dw` → Delete forward by word.
* `Esc + de` → Delete to the end of the current/next word.
* `Esc + dd` → Delete the entire current line.
* `Esc + d$` → Delete from the cursor to the end of the line.
* `Esc + d0` → Delete from the cursor to the beginning of the line.
* `Esc + D` → Delete from the cursor to the end of the line.
* `Esc + x` → Delete the character under the cursor.
* `Esc + X` → Delete the character before the cursor.

---

## 6. Undo / Redo

**Mode: Normal Mode**

> **Note:** Press **`Esc`** first to return from Insert Mode.

* `Esc + u` → Undo the last change.
* `Esc + Ctrl + r` → Redo an undone change.
* `Esc + U` → Undo all changes made to the current line.

---

## 7. Word Navigation

**Mode: Normal Mode**

> **Note:** Press **`Esc`** first to return from Insert Mode.

* `Esc + w` → Beginning of the next word.
* `Esc + e` → End of the current/next word.
* `Esc + b` → Beginning of the previous word.
* `Esc + ge` → End of the previous word.

---

## 8. Copy / Paste

**Mode: Normal Mode**

> **Note:** Press **`Esc`** first to return from Insert Mode.

### Copy / Yank

* `Esc + y` → Yank/copy selected text.
* `Esc + yy` → Copy the current line.
* `Esc + yw` → Copy from the cursor to the beginning of the next word.
* `Esc + ye` → Copy from the cursor to the end of the word.
* `Esc + yb` → Copy backward to the beginning of the previous word.
* `Esc + yge` → Copy backward to the end of the previous word.

### Paste

* `Esc + p` → Paste after the cursor.
* `Esc + P` → Paste before the cursor.

---

## 9. Selection in `vi`

**Mode: Normal Mode → Visual Mode**

> **Note:** Press **`Esc`** first to return from Insert Mode.

### Visual Modes

* `Esc + v` → Enter Character-wise Visual Mode.
* `Esc + V` → Enter Line-wise Visual Mode.

### Character-wise Selection

* `Esc + v + ↑` → Select upward.
* `Esc + v + ↓` → Select downward.
* `Esc + v + ↑ + ↑` → Select two positions upward.
* `Esc + v + ↓ + ↓` → Select two positions downward.

### After Selecting

* `y` → Copy/yank the selected content.
* `d` → Delete the selected content.

---

## 10. Select the Entire File

**Mode: Normal Mode → Visual Mode**

> **Note:** Press **`Esc`** first to return from Insert Mode.

### From First Line to Last Line

```text
Esc + gg + V + G
```

* `gg` → Go to the first line.
* `V` → Select the current line.
* `G` → Select until the last line.
* `y` → Copy the selected content.
* `d` → Delete the selected content.

### From Last Line to First Line

```text
Esc + G + V + gg
```

* `G` → Go to the last line.
* `V` → Select the current line.
* `gg` → Select until the first line.
* `y` → Copy the selected content.
* `d` → Delete the selected content.

---

## 11. Search a Word

**Mode: Normal Mode**

> **Note:** Press **`Esc`** first to return from Insert Mode.

### Forward Search

```text
Esc + /Linux
```

* `/Linux` → Search forward for `Linux`.
* `n` → Go to the next match.
* `N` → Go to the previous match.

### Easy Forward Search

* Place the cursor on the word.
* `Esc + *` → Search for the word forward.

### Backward Search

```text
Esc + ?Linux
```

* `?Linux` → Search backward for `Linux`.
* `n` → Go to the next match in the search direction.
* `N` → Go to the match in the opposite direction.

### Easy Backward Search

* Place the cursor on the word.
* `Esc + #` → Search for the word backward.

---

## 12. Search Only the Exact Word

**Mode: Normal Mode**

> **Note:** Press **`Esc`** first to return from Insert Mode.

If your file contains:

```text
Linux
LinuxServer
myLinux
Linux server
```

To search only the standalone word **`Linux`**:

```text
/\<Linux\>
```

For case-insensitive matching:

```text
/\<Linux\>\c
```

### Search Symbols

* `\<` → Beginning of the word.
* `\>` → End of the word.
* `\c` → Case-insensitive matching.

---

## 13. Indentation

**Mode: Normal Mode**

> **Note:** Press **`Esc`** first to return from Insert Mode to Normal Mode.

### Indent Current Line

```text
Esc + >>
```

* `>>` → Indent 1 line.

> **Note:** **`>>`** means press **`>` twice**.

### Indent Multiple Lines

The number before `>>` tells `vi` how many lines to indent, starting from the current line.

```text
Esc + 2>>
```

* `2>>` → Indent 2 lines.

```text
Esc + 4>>
```

* `4>>` → Indent 4 lines.

```text
Esc + 5>>
```

* `5>>` → Indent 5 lines.

### Remove Indentation

```text
Esc + <<
```

* `<<` → Remove indentation from 1 line.

```text
Esc + 2<<
```

* `2<<` → Remove indentation from 2 lines.

```text
Esc + 4<<
```

* `4<<` → Remove indentation from 4 lines.

```text
Esc + 5<<
```

* `5<<` → Remove indentation from 5 lines.

> **Note:** **`<<`** means press **`<` twice**.

### General Rule

```text
Esc + N>> → Indent N lines
Esc + N<< → Remove indentation from N lines
```

---

## 14. Select and Indent Multiple Lines

**Mode: Normal Mode → Visual Mode**

> **Note:** Press **`Esc`** first to return from Insert Mode to Normal Mode.

### Select Lines Downward

```text
Esc + gg + V + ↓ + >
```

* `gg` → Go to the first line.
* `V` → Select the entire current line.
* `↓` → Select the next line.
* `>` → Indent the selected lines.

### Select Lines Upward

```text
Esc + V + ↑ + >
```

* `V` → Select the current line.
* `↑` → Select the line above.
* `>` → Indent the selected lines.

### More Indentation

```text
Esc + V + ↑ + > + >
```

* First `>` → Add one level of indentation.
* Second `>` → Add another level of indentation.

> **Note:** Press **`>`** again to add more indentation levels.

### Remove Indentation

```text
Esc + V + ↑ + <
```

* `<` → Remove one level of indentation from the selected lines.

---

## 15. Empty Lines

**Mode: Normal Mode → Insert Mode**

> **Note:** Press **`Esc`** first to return from Insert Mode to Normal Mode.

* `Esc + o` → Create an empty line **below** the current line and enter Insert Mode.
* `Esc + O` → Create an empty line **above** the current line and enter Insert Mode.
* `Esc` → Return to Normal Mode after creating/editing the line.

### Create Multiple Empty Lines

* `Esc + o` → Create a new line below.
* Press `o` again → Create another new line below.
* Press `Esc` → Return to Normal Mode.

---

## 📄 Quick Reference

| Mode    | Command    | Function                        |
| ------- | ---------- | ------------------------------- |
| Normal  | `Esc`      | Return to Normal Mode           |
| Normal  | `Ctrl + D` | Scroll down                     |
| Normal  | `Ctrl + U` | Scroll up                       |
| Insert  | `i`        | Insert before cursor            |
| Insert  | `a`        | Insert after cursor             |
| Insert  | `Ctrl + U` | Delete backward                 |
| Insert  | `Ctrl + W` | Delete previous word            |
| Normal  | `x`        | Delete character                |
| Normal  | `dw`       | Delete forward by word          |
| Normal  | `D`        | Delete to end of line           |
| Normal  | `db`       | Delete backward by word         |
| Normal  | `>>`       | Indent 1 line                   |
| Normal  | `2>>`      | Indent 2 lines                  |
| Normal  | `4>>`      | Indent 4 lines                  |
| Normal  | `<<`       | Remove indentation              |
| Normal  | `2<<`      | Remove indentation from 2 lines |
| Normal  | `o`        | New line below                  |
| Normal  | `O`        | New line above                  |
| Normal  | `u`        | Undo                            |
| Normal  | `Ctrl + r` | Redo                            |
| Normal  | `yy`       | Copy current line               |
| Normal  | `p`        | Paste after cursor              |
| Normal  | `P`        | Paste before cursor             |
| Normal  | `gg`       | Go to first line                |
| Normal  | `G`        | Go to last line                 |
| Normal  | `/word`    | Search forward                  |
| Normal  | `?word`    | Search backward                 |
| Normal  | `*`        | Search word forward             |
| Normal  | `#`        | Search word backward            |
| Command | `:w`       | Save                            |
| Command | `:wq`      | Save and exit                   |
| Command | `:q!`      | Exit without saving             |

---

## 📖 Page Navigation

**Previous:** [← Terminal Keyboard Shortcuts](https://r-lakshman.github.io/Linux-System-Administrator/02-terminal-keyboard-shortcuts.html)

**Home:** [🏠 README](https://r-lakshman.github.io/Linux-System-Administrator/)

**Next:** —

---

## 🔗 Repository

[View On GitHub](https://github.com/r-lakshman/Linux-System-Administrator)

---

© 2026 R Lakshman Kumar. All rights reserved.

