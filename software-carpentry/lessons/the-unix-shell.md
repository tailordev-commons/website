# The UNIX shell

{% hint style='info' %}
You can find the Software Carpentry lesson at: https://swcarpentry.github.io/shell-novice/.
{% endhint %}

On this page, you will find:

<!-- toc -->

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

{% hint style='working' %}
These notes are mainly written for the instructors. Yet, they contain most (if not all) commands and important points taught during a workshop, which may be interesting if you want to remember how much you learnt during a workshop.
{% endhint %}

We tend to follow the [Software Carpentry schedule](https://swcarpentry.github.io/shell-novice/), but if time is lacking, we skip the loops (especially if the second day is dedicated to Python).

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

{% hint style='danger' %}
The `--help` option does not always work depending on the Operating System. It may work with `-h` or `man ls`.
{% endhint %}

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

Explain special directories like `..` and  `.`

```
$ cd ..
$ pwd
```

Option `-a` is for "show all":

```
$ ls -F -a
amino-acids.txt   elements/     pdb/	        salmon.txt
animals.txt       morse.txt     planets.txt     sunspot.txt
```

Talk about **hidden files**

**Action:** recap commands, options, and help.

```
$ ls
$ cd
$ pwd
```

Go directly where you want:

```
$ cd Desktop/data-shell/data
```

Talk about relative/absolute paths:

```
$ pwd
$ cd /Users/bebatut/Desktop/data-shell
```

Explain the following shortcuts: `~` and `-`.

**Action:** give link to zip file from a scientist called Nelle: [shell-novice-data.zip](/software-carpentry/data/shell-novice-data.zip).

### Organizing files

Explore the data.

Knowing just this much about files and directories, Nelle is ready to organize the files that the protein assay machine will create.

1. She creates a directory called `north-pacific-gyre`
2. She creates a directory called `2012-07-03`, which is the date she started processing the samples

Each of her physical samples is labelled according to her lab’s convention with a unique ten-character ID, such as “NENE01729A”. This is what she used in her collection log to record the location, time, depth, and other characteristics of the sample, so she decides to use it as part of each data file’s name. Since the assay machine’s output is plain text, she will call her files `NENE01729A.txt`, `NENE01812A.txt`, and so on. All 1520 files will go into the same directory.

**Question:** is it a relative/absolute path? Think about other challenge questions.

Talk about tab **completion**.

### Working with files and directories

How to create files and directories?

```
$ pwd # ensure we are in data-shell/
$ ls -F
```

**Question:** how to create a directory? we want to "make a directory".

```
$ mkdir thesis
$ ls -F
```

**Action:** show in the Finder

### Good names for files and directories

Common rules:

- Don't use whitespaces
- Don't begin the name with `-` (dash)
- Stick with letters, numbers, `.` (period), `-` (dash) and `_` (underscore)

```
$ ls -F thesis # empty, let's create a file!
$ cd thesis
```

Present the `nano` text only editor.

{% hint style='danger' %}
The _Git Bash_ users will not have `nano` installed but rather `vi`, which is complicated to use since it does not give any information on how to use it.
{% endhint %}

**Question:** what do you use to write a paper? or thesis?

```
$ nano draft.txt
```

Explain that Control = Ctrl = `^` key (hence the info in `nano`).

**Action:** write some content, then save and quit.

**Question:** where is your file? how to check?

```
$ ls
```

Removing a file (be careful, **no trash bin**):

```
$ rm draft.txt
$ ls
```

**Action:** try to remove a directory not empty by recreating the file first, then go to parent and `rm`.

```
$ pwd
$ nano draft.txt
$ ls
$ cd ..
$ rm thesis
```

Talk about recursively removing files, but tell the audience that it is dangerous. They should use interactive mode `-i`.

```
$ rm -r thesis
```

Create `draft.txt`:

```
$ pwd
$ mkdir thesis
$ nano thesis/draft.txt
$ ls thesis
```

Renaming a file by **moving** it:

```
$ mv thesis/draft.txt thesis/quotes.txt
$ ls thesis
```

`mv` is for files and directories (no `mvdir` for instance).

We can move files to directories too, but it does not transform a file into a directory, it moves the file somewhere else (physically):

```
$ mv thesis/quotes.txt .
$ ls thesis
```

See if the file is present:

```
$ ls quotes.txt
```

Copy files with `cp`:

```
$ cp quotes.txt thesis/quotations.txt
$ ls quotes.txt thesis/quotations.txt
```

Error expected if any of the files given to `ls` does not exist:

```
$ rm quotes.txt
$ ls quotes.txt thesis/quotations.txt
```

Create a file with `touch`:

```
$ touch new-file
$ ls
$ nano new-file
```

### Pipes and Filters

`wc` stands for word count.

`wc -l` for counting lines.

```
$ ls molecules
$ cd molecules
$ wc *.pdb
```

Wildcards `*` (zero or more characters) and `?` (a single character, not really used).

**Exercise ideas:** use wilcards

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

Redirection with `>` (which also creates the file if it does not already exist).

It **overwrites** the file if it exists and may lead to altered data.

```
$ wc -l *.pdb > lengths.txt
```

```
$ ls lengths.txt
```

`cat` for displaying the content of the file (concatenate):

```
$ cat lengths.txt
```

`sort` for sorting things (alphabetically).

`sort -n` means the sort is numerical instead of alphabetical:

```
$ sort -n lengths.txt
```

{% hint style='danger' %}
Sorting without `-n` gives different results depending on the Operating System, the locale, and maybe other things too. On some system, running `sort` without `-n` can give the expected result for sorting things numerically, but you should always specify the `-n` option if you intend to sort things numerically.
{% endhint %}

It does not change the file:

```
$ sort -n lengths.txt > sorted-lengths.txt
```

`head` for displaying the beginning (head) of the file (`-n 1` = first line):

```
$ head -n 1 sorted-lengths.txt
```

Redirecting to the same file is a very bad idea!

Too many intermediate files, solution is **pipe**:

```
$ sort -n lengths.txt | head -n 1
$ wc -l *.pdb | sort -n

$ wc -l *.pdb | sort -n | head -n 1
# head of sort of line count of *.pdb
```

Things worth explaining:

- Process
- Standard input
- Standard output

![](https://github.com/swcarpentry/shell-novice/raw/gh-pages/fig/redirects-and-pipes.png)

Sucess of Unix: creation of lots of simple tools that each do one job well and that work well with each other --> pipe and filter.

**Exercise ideas:**

- Nelle has run her samples through the assay machines and created 1520 files in the `north-pacific-gyre/2012-07-03` directory described earlier. She ask you to check that the number of lines is the same in all files as there should be 300 lines per file.

```
$ ls *Z.txt
```

### Loops

Loops: key productivity improvements through automation --> repetition of commands.

```
$ cd ../creatures
```

Only 2 files here, but the principe can be applied to many more files at once:

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

Follow the prompt!

Same symbols, different meanings: `>` and `$`:

- shell printing: typing expecting
- you typing, shell redirection or variable

```
$ for x in basilisk.dat unicorn.dat # name of variable
> do
>  head -n 3 $x
> done
```

{% hint style='danger' %}
This is a Bash `for` loop. It will not work as is on ZSH for instance (which is another shell).
{% endhint %}

```
$ for filename in *.dat
> do
>   echo $filename # explaining what is echo, importance of echo
>   head -100 $filename | tail -n 20
> done
```

Avoid whitespaces:

```
$ for filename in *.dat
> do
>   cp $filename original-$filename
> done
```

** Exercise ideas:**

- Processing files
  1. Check she select the right files: the onles whose names end in 'A' or 'B', rather than 'Z'
  2. Check what happen if you prefix each input file's name with "stats" (for the output of `goostats` program)
  3. Apply `bash goostats $input $output` to each file
  4. Apply `bash goostats` after adding an `echo` to check on which file it is running

### Shell scripts

Shell scripts are small programs.

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

### Finding things

`grep` stands for Global/Regular Expression/Print" --> find lines in files.

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

`find` is for finding files:

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