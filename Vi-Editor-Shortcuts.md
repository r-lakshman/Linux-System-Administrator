## Linux File Navigation and Editing Using vi Editor

### 1. Opening a File with `vi`

- To open a file with the `vi` editor:
  - `vi filename`
  - Example:
    - `vi test.txt`

- When `vi` opens, it starts in **Normal/Command mode**.
  - Press **`i`** to enter **Insert/Edit mode**.
  - You will see:
    - `-- INSERT --`
  - Now you can type or modify the contents of the file.

### 2. Insert/Edit Mode

- `i` → Insert before the cursor
- `a` → Insert after the cursor
- `o` → Open a new line below the current line

- To return to Normal/Command mode:
  - Press **`Esc`**

### 3. Command-Line Mode

- Press **`:`** from Normal mode.

- `:wq`
  - **Save and Exit**
  - Saves the file and exits `vi`.

- `:q!`
  - **Exit Without Saving**
  - Exits without saving changes.

- `:qa!`
  - **Quit all open files without saving changes**

- `:w`
  - **Save File Without Quitting**

- `:w filename`
  - **Save as a different filename without quitting**

### 4. Delete Commands

> **All of these commands are used in Normal mode.**
> If you're in Insert/Edit mode, press **`Esc`** first.

- **Delete**
  - `db` → Delete backward to the beginning of the previous word
  - `dw` → Delete from cursor to the beginning of the next word
  - `de` → Delete from cursor to the end of the current/next word
  - `dd` → Delete the entire current line
  - `d$` → Delete from cursor to the end of the line
  - `d0` → Delete from cursor to the beginning of the line
  - `D` → Delete from cursor to the end of the line
  - `x` → Delete character under the cursor
  - `X` → Delete character before the cursor

### 5. Navigation

- `0` → Beginning of the line
- `$` → End of the line
- `gg` → First line of the file
- `G` → Last line of the file
- `G$` → Last line, then move to the end of that line

> **Note:** `0` means beginning of the line, not sentence.

### 6. Undo / Redo

- `u` → Undo last change
- **`Ctrl + r`** → Redo undone change
- `U` → Undo all changes made to the current line

### 7. Word Navigation

- `w` → Beginning of the next word
- `e` → End of the current/next word
- `b` → Beginning of the previous word
- `ge` → End of the previous word

### 8. Copy / Paste

- **Copy / Yank**
  - `y` → Yank/copy selected text
  - `yy` → Copy the current line
  - `yw` → Copy from cursor to the beginning of the next word
  - `ye` → Copy from cursor to the end of the current/next word
  - `yb` → Copy backward to the beginning of the previous word
  - `yge` → Copy backward to the end of the previous word

- **Paste**
  - `p` → Paste after the cursor
  - `P` → Paste before the cursor

### 9. Selection in Vim

- `v` → Enter Visual mode
  - `v` + `↑` → Select upward
  - `v` + `↓` → Select downward
  - `v` + `↑ ↑` → Select two lines upward
  - `v` + `↓ ↓` → Select two lines downward

- After selecting:
  - `y` → Copy selected content
  - `d` → Delete selected content

- Visual modes:
  - `v` → Character-wise selection
  - `V` → Line-wise selection

### 10. Select the Entire File

- From the first line to the end:
  - `gg → v → G`
    - To copy → `y`
    - To delete → `d`

- From the last line to the start:
  - `G → V → gg`
    - To copy → `y`
    - To delete → `d`

### 11. Search a Word

- **Forward search:**
  - `/Linux`
  - `n` → Next match
  - `N` → Previous match

- **Easy method:**
  - Place cursor on the word
  - Press `*`

- **Backward search:**
  - `?Linux`
  - `n` → Next match in backward direction
  - `N` → Opposite direction

- **Easy method:**
  - Place cursor on the word
  - Press `#`

### 12. Search Only the Exact Word

If your file contains:

- `Linux`
- `LinuxServer`
- `myLinux`
- `Linux server`

To search only the standalone word **`Linux`**:

- `/\<Linux\>`

For case-insensitive matching:

- `/\<Linux\>\c`

### Search Symbols

- `\<` → Beginning of word
- `\>` → End of word
- `\c` → Case-insensitive matching

