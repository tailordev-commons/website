# The UNIX shell

{% hint style='info' %}
You can find the Software Carpentry lesson at: https://swcarpentry.github.io/shell-novice/.
{% endhint %}

## Introduction

### UNIX?

+ A family of Operating Systems
+ BSD, System V, Linux, MacOS

### The UNIX philosophy

> "the idea that the power of a system comes more<br>from the relationships among programs than from<br>the programs themselves"

..., which means:

+ write programs that do one thing and do it well
+ write programs to work together
+ write programs to handle text streams, because that is a universal interface

### Shell?

* a program that allows to talk to the computer
* powerful, fast, text-based
* ~~not really~~ beautiful

## Instructor notes

### Navigating Files and Directories

First, talk about the prompt (`$` / PS1)

```
$ whoami
$ # show `which` to say the shell runs X
$ pwd # print working directory
```

**Action:** draw the filesytem organization (`/` for root dir, inverted tree, different on Windows, file extensions are a convention)

**Action:** open Finder to see the files.

```
$ ls
Applications Documents    Library      Music        Public
Desktop      Downloads    Movies       Pictures
```

```
$ ls -F
Applications/ Documents/    Library/      Music/        Public/
Desktop/      Downloads/    Movies/       Pictures/
```

**Question:** how to get help?

```
$ ls --help
Usage: ls [OPTION]... [FILE]...
```

```
$ man ls
```

```
$ ls Desktop
data-shell/
```

**Action:** `ls` with and without argument/flag (most commands have flags)

```
$ ls Desktop/data-shell
creatures/          molecules/          notes.txt           solar.pdf
data/               north-pacific-gyre/ pizza.cfg           writing/
```

Navigating with `cd`:

```
$ cd Desktop
$ cd data-shell
$ cd data
$ pwd
$ ls
```

Error when not found:

```
$ cd data-shell
-bash: cd: data-shell: No such file or directory
```

:fa-info-circle: explanation about `..` and  `.`

```
$ cd ..
$ pwd
```

:fa-info-circle: `-a` is for "show all"


```
$ ls -F -a
amino-acids.txt   elements/     pdb/	        salmon.txt
animals.txt       morse.txt     planets.txt     sunspot.txt
```

:fa-info-circle: talk about **hidden files**

**Recap'**

```
$ ls
$ cd
$ pwd
```

:fa-info-circle: go directly where you want

```
$ cd Desktop/data-shell/data
```

:fa-info-circle: talk about relative/absolute paths:

```
$ pwd
$ cd /Users/bebatut/Desktop/data-shell
```

:fa-info-circle: 2 more shortcuts: `~` and `-`

:fa-edit: give link to zip file from a scientist called Nelle https://swcarpentry.github.io/shell-novice/data/shell-novice-data.zip

### Organizing files

:fa-info-circle: explore the data

Knowing just this much about files and directories, Nelle is ready to organize the files that the protein assay machine will create.

1. She creates a directory called `north-pacific-gyre`
2. She creates a directory called `2012-07-03`, which is the date she started processing the samples

Each of her physical samples is labelled according to her lab’s convention with a unique ten-character ID, such as “NENE01729A”. This is what she used in her collection log to record the location, time, depth, and other characteristics of the sample, so she decides to use it as part of each data file’s name. Since the assay machine’s output is plain text, she will call her files `NENE01729A.txt`, `NENE01812A.txt`, and so on. All 1520 files will go into the same directory.

:fa-bullhorn: ask questions like "is it a relative/absolute path?"

:fa-info-circle: talk about tab **completion**

---

# Working with files and directories

How to create files and directories?

```
$ pwd # ensure we are in data-shell/
$ ls -F
```

:fa-bullhorn: how to create a directory? we want to "make a directory"

```
$ mkdir thesis
$ ls -F
```

:fa-edit: show in the Finder

### Good names for files and directories

- Don't use whitespaces
- Don't begin the name with `-` (dash)
- Stick with letters, numbers, `.` (period), `-` (dash) and `_` (underscore).

```
$ ls -F thesis # empty, let's create a file!
$ cd thesis
```

:fa-info-circle: `nano` text only editor

:fa-bullhorn: what do you use to write a paper? or thesis?

```
$ nano draft.txt
```

:fa-info-circle: Control == Ctrl == `^` key (hence the info in `nano`)

:fa-info-circle: write some content, then save and quit

:fa-bullhorn: where is your file? how to check?

```
$ ls
```

Removing a file (be careful, **no trash bin**):

```
$ rm draft.txt
$ ls
```

:fa-info-circle: try to remove a directory not empty by recreating the file first, then go to parent and `rm`

```
$ pwd
$ nano draft.txt
$ ls
$ cd ..
$ rm thesis
```

:fa-info-circle: recursively removing files:

:fa-warning: that is dangerous, use interactive mode `-i`

```
$ rm -r thesis
```

:fa-info-circle: create `draft.txt`

```
$ pwd
$ mkdir thesis
$ nano thesis/draft.txt
$ ls thesis
```

:fa-info-circle: renaming a file by **moving** it

```
$ mv thesis/draft.txt thesis/quotes.txt
$ ls thesis
```

:fa-info-circle: `mv` is for files and directories (no `mvdir` for instance)

:fa-info-circle: we can move files to directories too, but it does not transform a file into a directory, it moves the file somewhere else (physically)

```
$ mv thesis/quotes.txt .
$ ls thesis
```

:fa-info-circle: see if the file is present

```
$ ls quotes.txt
```

:fa-info-circle: copy files with `cp`

```
$ cp quotes.txt thesis/quotations.txt
$ ls quotes.txt thesis/quotations.txt
```

:fa-info-circle: error expected if any of the files given to `ls` does not exist

```
$ rm quotes.txt
$ ls quotes.txt thesis/quotations.txt
```

:fa-info-circle: create a file with `touch`

```
$ touch new-file
$ ls
$ nano new-file
```

---

# Pipes and Filters

:fa-info-circle: `wc` stands for word count

:fa-info-circle: `wc -l` for counting lines

```
$ ls molecules
$ cd molecules
$ wc *.pdb
```

:fa-info-circle: wildcards `*` (zero or more characters) and `?` (a single character, not really used)

> Exercise: Using wilcards

--

```
$ wc -l *.pdb
  20  cubane.pdb
  12  ethane.pdb
   9  methane.pdb
  30  octane.pdb
  21  pentane.pdb
  15  propane.pdb
 107  total
```

Which of these files is shortest? It’s an easy question to answer when there are only six files, but what if there were 6000?

:fa-info-circle: redirection with `>` (which also creates the file if it does not already exist)

:fa-warning: it **overwrites** the file if it exists

```
$ wc -l *.pdb > lengths.txt
```

```
$ ls lengths.txt
```

:fa-info-circle: `cat` for displaying the content of the file (concatenate)

```
$ cat lengths.txt
```

:fa-info-circle: `sort` for sorting things

:fa-info-circle: `sort -n` means the sort is numerical instead of alphabetical

```
$ sort -n lengths.txt
```

:fa-warning: it does not change the file

```
$ sort -n lengths.txt > sorted-lengths.txt
```

:fa-info-circle: `head` for displaying the beginning (head) of the file (`-n 1` == first line)

```
$ head -n 1 sorted-lengths.txt
```

:fa-warning: Redirecting to the same file is a very bad idea!

:fa-info-circle: too many intermediate files, solution is **pipe**

```
$ sort -n lengths.txt | head -n 1
$ wc -l *.pdb | sort -n

$ wc -l *.pdb | sort -n | head -n 1
# head of sort of line count of *.pdb
```

- Process
- Standard input
- Standard output

![](https://github.com/swcarpentry/shell-novice/raw/gh-pages/fig/redirects-and-pipes.png)

Sucess of Unix: creation of lots of simple tools that each do one job well and that work well with each other --> pipe and filter

> Exercise: Checking files
> Nelle has run her samples through the assay machines and created 1520 files in the `north-pacific-gyre/2012-07-03` directory described earlier
> She asked you to check the number of lines is the same in all files 
> as there is supposed to be 300 lines per file

```
$ ls *Z.txt
```

> Exercises

---

# Loops

Loops: key productivity improvements through automation --> repetition of commands

```
$ cd ../creatures
```

Only 2 files here, but the principe can be applied to many more files at once

```
$ cp *.dat original-*.dat # can not be used
$ cp basilisk.dat unicorn.dat original-*.dat # expanding version
```

```
$ for filename in basilisk.dat unicorn.dat
> do
>   head -n 3 $filename
> done
```

- Follow the prompt
- Same symbols, different meanings: `>` and `$`
	- shell printing: typing expecting
    - you typing, shell redirection or variable

```
$ for x in basilisk.dat unicorn.dat # name of variable
> do
>  head -n 3 $x
> done
```
```
$ for filename in *.dat
> do
>   echo $filename # explaining what is echo, importance of echo
>   head -100 $filename | tail -n 20
> done
```

Avoid whitespaces

```
$ for filename in *.dat
> do
>   cp $filename original-$filename
> done
```

> Exercise: Processing files
> 1. Check she select the right files: the onles whose names end in 'A' or 'B', rather than 'Z'
> 2. Check what happen if you prefix each input file's name with "stats" (for the output of `goostats` program)
> 3. Apply `bash goostats $input $output` to each file
> 4. Apply `bash goostats` after adding an `echo` to check on which file it is running

- Up-arrow
- Ctrl-C
- Ctrl-A and Ctrl-E
- Ctrl-R
- `!!`
- `!$`

> Exercises

# Shell scripts

Shell scripts: small programs

```
$ cd ../molecules
$ nano middle.sh
	head -n 15 octane.pdb | tail -n 5
$ bash middle.sh
```
```
$ nano middle.sh
	head -n 15 "$1" | tail -n 5
$ bash middle.sh octane.pdb
$ bash middle.sh pentane.pdb
```
```
$ nano middle.sh
	head -n "$2" "$1" | tail -n "$3"
$ bash middle.sh pentane.pdb 15 5
$ bash middle.sh pentane.pdb 20 5
```
```
$ nano middle.sh
	# Select lines from the middle of a file
    # Usage: bash middle.sh filename end_line num_line
    head -n "$2" "$1" | tail -n "$3"
```

```
$ wc -l *.pdf | sort -n
```
```
$ nano sorted.sh
	# Sort filenames by their length
    # Usage: bash sorted.sh one_or_more_filenames
    wc -l "$@" | sort -n
$ bash sorted.sh *.pdb ../creatures/*.dat
```
```
$ history | tail -n 5 > redo-figure-3.sh
```

> Exercise: Creating a script for Nelle's pipeline
> An off-hand comment from her supervisor has made Nelle realize that she should have provided a couple of extra parameters to goostats when she processed her files. This might have been a disaster if she had done all the analysis by hand, but thanks to for loops, it will only take a couple of hours to re-do.

> Exercises

# Finding things

`grep`: "global/regular expression/print" --> find lines in files

```
$ cd writing
$ cat haiku.txt
```
```
$ grep not haiku.txt
$ grep The haiku.txt # in larger words: Thesis
$ grep -w The haiku.txt
$ grep -w "is not" haiku.txt
```
```
$ grep -n "it" haiku.txt
```
```
$ grep -n -w "the" haiku.txt
```
```
$ grep -n -w -i "the" haiku.txt #case insensitive
$ grep -n -w -v "the" haiku.txt #inverted search
$ grep --help
```

Wildcards

`find`: find files

```
$ find .
```
```
$ find . -type d
$ find . -type f
```
```
$ find . -name *.txt # run: find . -name haiku.txt
$ find . -name '*.txt'
```
```
$ wc -l $(find . -name '*.txt')
$ grep "FE" $(find .. -name '*.pdb')
```

> Exercises
