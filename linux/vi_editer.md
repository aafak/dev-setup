# Basic Usage of vi
# 1. Open a file in vi
 - vi filename : If the file does not exist, vi will create it.

# 2. Switch to Insert Mode
- Press i → Insert text before the cursor.
- Press a → Insert text after the cursor.
- Press o → Open a new line below.
- Press O → Open a new line above.

# 3. Exit Insert Mode
 - Press Esc to return to Normal Mode.

#4. Save and Exit
- :w → Save (Write) changes.
- :q → Quit.
- :wq or ZZ → Save and Quit.
- :q! → Quit without saving.

# Navigation in Normal Mode
- h → Move left
- l → Move right
- j → Move down
- k → Move up
- 0 → Move to the beginning of the line
- $ → Move to the end of the line
- gg → Move to the beginning of the file
- G → Move to the end of the file
- :n → Go to line n (e.g., :10 moves to line 10)

# Editing Commands
- x → Delete a character.
- dd → Delete a line.
- yy → Copy (yank) a line.
- p → Paste after the cursor.
- P → Paste before the cursor.
- u → Undo last change.
- Ctrl + r → Redo.
- Search and Replace
- /pattern → Search forward for pattern.
- ?pattern → Search backward for pattern.
- n → Repeat the search in the same direction.
- N → Repeat the search in the opposite direction.
- :%s/old/new/g → Replace all occurrences of old with new.
:10,20s/foo/bar/g → Replace foo with bar in lines 10 to 20.
