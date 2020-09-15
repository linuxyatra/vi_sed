
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


