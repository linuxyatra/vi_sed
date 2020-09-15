# Working on Unix/Linux

I have been using Linux OS for some time now, for research and my other work related stuffs. Here I am sharing my notes.

Vi Editor basically has two modes: **INSERT MODE** and **COMMAND MODE**. In Insert mode, one can edit, make changes. On the other hand in command mode, we can enter commands to perform certain task, for example substitution, deletion.

* To switch from **INSERT MODE** to **COMMAND MODE** press **Esc** key.

* To switch from **COMMAND MODE** to **INSERT MODE** press **I**.

## Basics commands 


```
i    : Insert text at the current cursor position
I    : Insert text at the begining of the current line.
o    : Add text in a new line below the current line.
O    : Add text in a new line above the current line.
a    : Append text after the position of cursor.
A    : Append at the end of line. 
```

* Move Cursor

```
h    : Move the cursor one character to the left 
l    : Move the cursor one character to the right
k    : Move the cursor up one line
j    : Move the cursor down one line
gg   : Go to the begining of file.
G    : Go to the end of the file.
^d   : Shift one page down [^: CTRL]
^u   : Shift one page up [^: CTRL]  
$    : Move cursor to the end of current line
0    : Move cursor to the beginning of current line
w    : Forward one word
b    : Backward one word 
```



* Cut / Copy / Paste

* Delete

```
x   : Delete a character
dd  : Delete current line
d$  : Delete from the position of the cursor to end of the line
dw  : Delete word from cursor on
db  : Delete word backward
```

* Copy (Yank)

```
yy  : Yank current line
y$  : Yank to end of current line from cursor
yw  : Yank from cursor to end of current word
2yy : Yank 2 lines
y   : Yanks the Highlighted characters.
```

* Paste

```
p  : Paste below the cursor
P  : Paste above the cursor
u  : Undo last change
U  : Restore line
J  : Join next line down to the end of the current line
```

* Highlight characters

```
v   : activates the visual mode and one can move cursor to highlight required characters.
^v  : Highlight vertically. Very useful for inserting tab in multiple lines.
```



* Exit from the Editor

```
:wq    : Write file to disk and quit the editor
:q!    : Quit (Without saving the changes)
:q     : Quit (Will print out a warning if changes have been made)
:w abc : Save the current file to a new file abc
```



## more commands 


* **Find and Replace**

One of the widely used commands for me personally.

```
:[range]s/{pattern}/{string}/[flags] [count]
```
**Possible Flags:**

[c]    : Confirm each substitution

[g]    : Replace all occurrrences in the line.

[i]      :  Ignore case for the pattern

s   :  stands for substitute


* Some examples 

```
:s/XX/YY/g         [only in current line]
:%s/XX/YY/g        [in the entire file]
:5,12s/XX/YY/g     [only in specific lines 5 and 12]
:.,$s/XX/YY/g      [current + all the following lines.]
:s/XX/YY/g 4       [Current + following 4 lines]
:.,+2s/XX/YY/g     [current + next 2 lines same as above.]

```

Explanation

**:s** for substitution, **.** : current line , **$** :end line, **%** : entire file, **g** : global search but locally global. only for that line.


* **insert spaces or indentation in multiple lines**

```
highlight the line[s] and press >> or <<
```

* deleting certain parts

```
:%normal 2x     [Delete the first n characters of every lines]
:%s/^ /         [Delete the first n characters of every lines only if they are spaces]
:%s/\s+$//e     [Delete any trailing space at the end of all the lines]
:%s/
:%s/^\s\+//e    [Delete all initial spaces(or tabs) of all the lines]
                [^: begining of line; \s looks for spaces(including tabs); \+ looks for one and or more occurance; //e: first / means substitute by and nothing after it means nothing and \e means if not found the string then suppress the error.]
:%le [==:left]           [Global left alignment (much more efficient)]

```

* OPEN/ CLOSE/ SPLIT  files


```
vim f1.txt             [open single file]
vim -o f1.txt f2.txt   [open two files in horizontal]
vim -O f1.txt f2.txt   [open two files vertically]
CTRL w [R/L/T/B arrow] [toggle between different split windows]
CTRL +w w              [  Toggle between different split windows]
:e new_file            [open new file in this window]

:sp new_file           [splits Horizontally and opens the new file]
:vsp new_file          [splits vertically and opens the new file]

CTRL +w , s            [split Horizontally ]  
CTRL +w , v            [split vertically ]
CTRL +w, Q             [Quit the current window]
```

* **g**lobal **command**

The global command is useful in many cases.

general pattern:

```
:[range]g/pattern/cmd
```
!!Examples

```
:g/[abcde]/d           [delete lines matching pattern abcde]
:!g/[abcde]/d          [delete lines not matching the pattern abcde]
:g/^\s*$/d             [^($) means start(end) of line and \s* means 0 or many spaces including tab, delete all empty lines.]
:g/[pat]/s/abc/def/gi  [In all lines containing pattern pat, substitute abc by def.]
```



* Find a pattern in a line and delete everything after it. or delete after that pattern

```
:1,$s/pattern.*//g .  # to delete everything after  (and including) that pattern
:1,$s/pattern.*/pattern/g .  # to delete everything after  (excluding) that pattern
```



* **Some other Examples**

Sometime you have to comment few lines. For that Usually for bash-script we put a # sign in the front of every line to comment that line. Easier way is following:
go to top(bottom) of the lines press **CTRL v** to go to **visual mode** and press **j** or **k** to go down or up to whatever many lines you need to comment. Press **I** (capital i) and put a sign **#** now go to command mode by pressing **Esc** key and save the file **:w**. Should work!



### Playing with tab and spaces in VIM
A lot of times I get old scripts and codes where a tab is used and while making changes and compiling the code I get indentation error due to tabs. Here is how to fix this.

* Replace tab by spaces: `:retab`
* Set length of spaces for a tab: `:set tabstop=4`,  `:set shiftwidth=4`, `:set expandtab`
* For more info, find my `.vimrc` file [my vimrc file](https://gitlab.com/khanalg44/All_dot_files/blob/master/vimrc_pc_khanal)

## Yank and Paste same thing multiple times.

`xnoremap p pgvy` **p** to paste, **gv** to re-select what was originally selected. **y** to copy it again.


## Grep and Egrep

### commands

```
-i            [ignore case]
-v            [invert the match]
-o            [only the matching]
-A [num]      [print the [num] lines after the match]
-B [num]      [print the [num] lines before the match] 
```



* First grep something from a file and then find the last line from that grepped file.

```
find FeSe.scf |xargs grep FGL002 |tail -1
```
Finds **FGL002** in file **.scf** and returns the last line 

* Find only specific numbers from a line

```
less log.ctqmc | egrep -o "<Sz>=-?[0-9].[0-9]+" | egrep -oe ’-?[0-9].[0-9]+’ > sz_data
```

* Find only the numbers from the grepped entity. use regular expression. egrep is for extended grep.

```
find FeSe.scf |xargs grep :FER |tail -1| egrep -o [0-9].[0-9]+
```



!Regular Expressions

```
^[-+]?[0-9]*\.?[0-9]+$
  
  ^ - start of string
  $ - the end of string
  [0-9]? - 0 or 1 sign indicator
  [0-9]*  - 0 or more integers
  [0-9]+  - 1 or more integers
  \.  - the charcter (. is used in regex to mean "any character")
```




## Sed and Awk

### **Commands**

* **p** print
* **d** delete
* **s** substitute
* **a** append
* **i** insert
* **c** change
* **y** transform
* **q** quit

!!**Things to note**

* **$** represents the last line
* **^$** represents blank line.


### **sed Syntax**

```
sed [-n] [-e] ['command'] [file]
```
* **-n** only prints line specified with the print command
* **-e** The next argument is a filename containing editing commands


### **print** 

Command **p** [**p**rint only certain lines]

```
Syntax:    [address1[,address2]]p
```

**Examples:**

```
sed -n '5,10p' file.dat     Print lines from line 5 to line 10
sed -n '5p' file.dat        Print only 5th line
sed -n '5,$p' file.dat      Print lines from 5th to last line
```

### **delete**

Command **d** [**d**elete certain line]

```
Syntax:    [address1[,address2]]d
```

!!Examples:

```
sed '5d' file.dat           [Delete line 5 while printing]
sed '5,10d' file.dat        [Delete lines from 5th to 10th while printing]
sed '/^$d' file.dat         [Delete line 5 while printing]
sed '/^$/,$d' file.dat      [Delete from first blank line through last line.]
sed '/str/,$d' file.dat     [Delete all lines after the line containing string **str**. [Also has to be single quotation mark.]
```

### **Substitute**

Command **s** [**s**ubstitute **AA** by **BB**]

```
Syntax:    [address(es)]s/pattern/replacement/[flags]
           flags: n   [nth occurrence]
                : g   [global occurrence]
```

### Examples:

```
sed ‘s/ AA/ BB/’ file.dat      Only the first occurrence
sed ‘s/ AA/ BB/g’ file.dat     global (all) occurrences
sed -i ‘s/ AA/ BB/g’ file.dat     replace in file (all) occurrences
```

* For a pattern which occurs multiple times in a file, replace only some of them. [Remember sig.inp for ferromagnetic calculations]


```
sed 's/AA/BB/2'                Replace only 2nd occurrence
sed 's/AA/BB/2g'               Replace all after 2nd occurrence
```

!!Note: while using sed in bash shell, be careful about '{text}' and "{text}" the later has been useful. Learn when to use one and when the other.

**More information can be on**

A great course for learning UNIX
http://www.cs.nyu.edu/~mohri/unix08/

Basic Unix commands
http://unixcommandstutorial.blogspot.com/2013/04/unixawkperl-sqlplsql-examples.html


some tutorials on awk 
http://www.grymoire.com/Unix/Awk.html#uh-14


## **awk**

awk can be as useful as sed and in many cases even better. 

* print only some columns of some output

```
awk '{print $2}' file.txt                 [print 2nd column]
grep 'str' file.txt |awk '{print $2}'     [print 2nd column of the output]
grep 'str' file.txt |awk '{print $2 $3}'  [print 2nd and 3rd column]
```

* print only some rows from file

```
awk 'NR==1{print}' file.txt          [print 1st line]
awk 'NR==1;END{print}' file.txt      [print first and last line.]
awk 'NR==1;END{print $2}' file.txt   [print 2nd column of first and last line.]
```

* find pattern and print only certain column

```
awk '/pattern/{print $1}' file    [find lines with pattern and print first column]
```


!Sed/Awk inside a bash script

Insied a bash script you have to be little careful using sed and awk, especially if you are using a variable inside a sed command. For example the following command inside a bash script
`sed -i 's/${var1}/${var2}' filename.dat`
**won't work**. First thing is it needs double quotes `**` as opposed to single quotes `'` and the second thing is the `/` sign must be replaced by apersand  symbol `&`. So the correct command would be `sed -i **s&${var1}&${var2}&g** filename.dat`


### Sed deleting last n lines of a file 

* **Option1: delete one line at a time for n times.** very expensive for large files. 

```
for i in `seq 1 n`; do
    sed -i '${d}' file.txt
```

* **Option2: print the file in reverse using ``tac`` and cut the first n lines and reverse the file once again using ``tac``.**

```
tac file.txt |sed '1,n{d}' |tac  > file_tmp
mv file_tmp file.txt
```

* **Option3: Found in the webpage  [sedoneliner](http://www.unixguide.net/unix/sedoneliner.shtml)**

```
sed -i -e :a -e '$d;N;2,4ba' -e 'P;D' test_file
```

* **Some other nice comands**

```
sed -i -e "1,${n0}d" $f        # works  to delete lines from 1 to n0
 sed -i -e "${n0},${n1}d" $f   # deletes lines from n0 to n1
```


# Git commands (basics)

## The most basic steps

* Initialize a project

Initializing a new project. First go to the project in Gitlab web page and start a new project. 

```
For Existing directory
cd existing_folder
git init
git remote add origin git@gitlab.com:khanalg44/Cif2Struct.git
git add .
git commit
git push -u origin master
```



* To clone a new project to the terminal

```
git clone <path of the repository>
git clone git@gitlab.com:khanalg44/project_name.git
```

* To pull the files from the git  `` git pull ``
* To check the status of the files ``git status``
* To update/save a new change

```
git add <filename> or git add .  # Add the file/files that you want to push to repo.
git commit -m 'some message      # Commit the changes with some message .
git push -u origin master        # Push the file to the main repo
```


### Questions/Error 

### Key Error

If you have public key error Follow the steps:

* 1st generate new key 
* `ssh-keygen -t rsa -C "khanalg44@gmail.com" -b 4096`
* Or simply create the ssh-public-key by `ssh-keygen -t rsa`
* copy the key from id_rsa.pub to the settings in gitlab.com-> profile -> settings -> SSH keys -> paste your key here
* click ``add key``
* Now reload your git webpage. And now git pull, git push should work.

### How to add branches in a git repository?

* [here is a nice webpage for this](https://services.github.com/on-demand/github-cli/create-branches-git)
* In short, here are the steps, 

```
git branch <branchname>
git status
git checkout <branchname>   #To go into the new branch
git push origin <branchname>
```




### Reference
* http://rogerdudler.github.io/git-guide/
* https://bitbucket.org/dasarpmar/tutorial/overview
* https://www.atlassian.com/git/tutorials/setting-up-a-repository/git-init


























