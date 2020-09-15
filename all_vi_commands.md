# VIM Editor Commands

Vim is an editor to create or edit a text file. There are two modes in vim. One is the command mode and another is the insert mode.

- In the `command` mode, user can move around the file, delete text, etc.
- In the `insert` mode, user can insert text.

**Changing mode from one to another**

- From command mode to insert mode type a/A/i/I/o/O ( see details below)
- From insert mode to command mode type Esc (escape key)

## Most commonly used commands

**Highlight characters**

- **v**   : activates the visual mode and one can move cursor to highlight required characters.
- **^v**  : Highlight vertically. Very useful for inserting tab in multiple lines.

**Find and Replace**

- **:[range]s/{pattern}/{string}/[flags] [count]** syntax
  - Example: **:.,+2s/XX/YY/g**    Substitute XX by YY in current + next 2 lines.
  - Example: **:.,$s/XX/YY/g**  Current + all the following lines.

**OPEN/CLOSE Multiple files**

- vim f1.txt             [open single file]
- vim -o f1.txt f2.txt   [open two files in horizontal]
- vim -O f1.txt f2.txt   [open two files vertically]
- CTRL w [R/L/T/B arrow] [toggle between different split windows]
- CTRL +w w              [  Toggle between different split windows]
- :e new_file            [open new file in this window]
- :sp new_file           [splits Horizontally and opens the new file]
- :vsp new_file          [splits vertically and opens the new file]
- CTRL +w , s            [split Horizontally ]  
- CTRL +w , v            [split vertically ]
- CTRL +w, Q             [Quit the current window]

* **Find and delete**

- **:1,$s/pattern.*//g .**  [to delete everything after  (and including) that pattern
- **:1,$s/pattern.*/pattern/g .**  [to delete everything after  (excluding) that pattern


**deleting certain parts**

- **:%normal 2x**     [Delete the first n characters of every lines]
- **:%s/^ /**         [Delete the first n characters of every lines only if they are spaces]
- **:%s/\s+$//e**     [Delete any trailing space at the end of all the lines]
- **:%s/**
- **:%s/^\s\+//e**    [Delete all initial spaces(or tabs) of all the lines]
  - [^: begining of line; \s looks for spaces(including tabs); \+ looks for one and or more occurance; //e: first / means substitute by and nothing after it means nothing and \e means if not found the string then suppress the error.]
- **:%le** **[==:left]**           [Global left alignment (much more efficient)]



## More detailed set of commands

**Text Entry Commands** (Used to start text entry)

- **a** Append text following current cursor position
- **A** Append text to the end of current line
- **i** Insert text before the current cursor position
- **I** Insert text at the beginning of the cursor line
- **o** Open up a new line following the current line and add text there
- **O** Open up a new line in front of the current line and add text there

The following commands are used only in the commands mode.

**Cursor Movement Commands**

- **h** Moves the cursor one character to the left
- **l** Moves the cursor one character to the right
- **k** Moves the cursor up one line
- **j** Moves the cursor down one line
- **nG **or **:n** Cursor goes to the specified (n) line (ex. 10G goes to line 10)
- **^F** (CTRl F) Forward screenful
- **^B** Backward screenful
- **^f** One page forward
- **^b** One page backward
- **^U** Up half screenful
- **^D** Down half screenful
- **$** Move cursor to the end of current line
- **0** (zero) Move cursor to the beginning of current line
- **w** Forward one word
- **b** Backward one word

**Exit Commands**

- **:wq** Write file to disk and quit the editor
- **:q!** Quit (no warning)
- **:q **Quit (a warning is printed if a modified file has not been saved)
- **ZZ** Save workspace and quit the editor (same as :wq)
- **: 10,25 w temp**  write lines 10 through 25 into file named temp. Of course, other line numbers can be used. (Use :f to find out the line numbers you want.

**Text Deletion Commands**

- **x**  Delete character
- **dw** Delete word from cursor on
- **db** Delete word backward
- **dd** Delete line
- **d$** Delete to end of line
- **d^** (d caret, not CTRL d) Delete to beginning of line

**Yank (has most of the options of delete)-- VI's copy commmand**

- **y$** yank to end of current line from cursor
- **yw** yank from cursor to end of current word
- **5yy** yank, for example, 5 lines

**Paste (used after delete or yank to recover lines.)**
- **p** paste below cursor
- **P** paste above cursor
- **"2p** paste from buffer 2 (there are 9)
- **u** Undo last change
- **U** Restore line
- **J** Join next line down to the end of the current line

**File Manipulation Commands**

- **:w** Write workspace to original file
- **:w** file Write workspace to named file
- **:e** file Start editing a new file
- **:r** file Read contents of a file to the workspace 
- To create a page break, while in the insert mode, press the CTRL key and l. ^L will appear in your text and will cause the printer to start a new page.

**Other Useful Commands**

Most commands can be repeated n times by typing a number, n, before the command. For example 10dd means delete 10 lines.

**Repeat last command**

- **cw** Change current word to a new word
- **r** Replace one character at the cursor position
- **R** Begin overstrike or replace mode � use ESC key to exit
- **:/** pattern Search forward for the pattern
- **:?** pattern Search backward for the pattern
- **n** (used after either of the 2 search commands above to continue to find next occurrence of the pattern.
- **:g/pat1/s//pat2/g** replace every occurrence of pattern1 (pat1) with pat2
  - Example **:g/tIO/s//Ada.Text_IO/g** This will find and replace tIO by Ada.text_IO everywhere in the file.

- **:g/a/s// /g** replace the letter a, by blank
- **:g/a/s///g** replace a by nothing note: Even this command be undone by u

## Examples

**Opening a New File**

- Step 1 type vim filename (create a file named filename)
- Step 2 type i ( switch to insert mode)
- Step 3 enter text (enter your Ada program)
- Step 4 hit Esc key (switch back to command mode)
- Step 5 type :wq (write file and exit vim)

 

**Editing the Existing File**

- Step 1 type vim filename (edit the existing file named filename)
- Step 2 move around the file using h/j/k/l key or any appropriate command
  - h Moves the cursor one character to the left
  - l Moves the cursor one character to the right
  - k Moves the cursor up one line
  - j Moves the cursor down one line
  - nG or :n Cursor goes to the specified (n) line
  - (ex. 10G goes to line 10)
- Step 3 edit required text (replace or delete or insert)
- Step 4 hit Esc key (exit from insert mode if you insert or replace text)
- Step 5 type :wq
