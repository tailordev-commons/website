# Introduction to programming with Python

{% hint style='info' %}
You can find the Software Carpentry lesson at: https://swcarpentry.github.io/python-novice-inflammation/. Nonetheless, we believe **the SC lesson does not target complete beginners** to programming. That is why we do not use its content and we have developed our own materials.
{% endhint %}

On this page, you will find:

<!-- toc -->

## Python 101

This lesson is an introduction to programming and the Python programming language. **This lesson targets complete beginners**. We start by typing a few lines of code in the Python shell and then use the **Jupyter Notebook**, an open-source web application that allows you to create and share documents that contain live code, equations, visualizations and explanatory text.

You can download the Jupyter Notebook for this lesson: [python-101.ipynb](/software-carpentry/data/python-101.ipynb). GitHub allows to preview its content if you just want to know what is in this notebook: [click here to see this notebook on GitHub](https://github.com/tailordev-commons/website/blob/master/software-carpentry/data/python-101.ipynb).

## Python 102

This lesson aims at plotting figures with [Matplotlib](http://matplotlib.org/) and using [NumPy](http://www.numpy.org/), the fundamental package for scientific computing with Python. This lesson has been created by [Björn Grüning](https://twitter.com/bjoerngruening). Now that you know the basics of programming with Python, let's have some fun with nice charts!

You can download the Jupyter Notebook for this lesson: [python-102.ipynb](/software-carpentry/data/python-102.ipynb). GitHub allows to preview its content if you just want to know what is in this notebook: [click here to see this notebook on GitHub](https://github.com/tailordev-commons/website/blob/master/software-carpentry/data/python-102.ipynb).

## Jupyter Notebook

[The Jupyter Notebook](https://jupyter.org/) (formerly known as the IPython Notebook) is an interactive computational environment, in which you can combine code execution, rich text, mathematics, plots and rich media.

{% hint style='working' %}
There is a public demo at: http://try.jupyter.org/. Yet, it is not always up and you should not use it during a workshop. It is better to setup a dedicated Jupyter instance.
{% endhint %}

When you open the Jupyter Notebook, you get redirect to your own **workspace**, that is a virtual filesystem where you can upload your notebooks, create files, and organize them as you wish. Each user gets its own workspace to avoid collisions:

![](/software-carpentry/assets/tryjupyter.png)

### Uploading a notebook

You can upload the notebooks we provide by clicking on "Upload" on the right, which opens a file explorer. Select the notebook you want to upload:

![](/software-carpentry/assets/jupyter_upload.png)

Confirm the file upload by clicking the blue "Upload" button again. The Jupyter Notebook gives you the ability to rename the file into your workspace here, but it is optional:

![](/software-carpentry/assets/jupyter_upload_confirm.png)

Once uploaded, you should see the uploaded notebook into your workspace:

![](/software-carpentry/assets/jupyter_upload_done.png)

You can open this notebook by clicking on it. For instance, the screenshot below is what you should see by opening the [Python 101](#python-101) notebook we provide:

![](/software-carpentry/assets/jupyter_python_101.png)

### Playing with a notebook

So far, you have uploaded and opened a notebook. Now, you probably want to use it. When you open a notebook, you get an editor _à la_ Microsoft Word or Google Doc (well, with the exception that Jupyter is more powerful as you can execute code and it is Open Source).

A notebook is usually configured for a specific programming language. If you use the Python notebooks we provide, then the configured programming language is set to `Python 3` (this information is displayed on the top right corner). If you start a new notebook, Jupyter will ask you which programming language you intend to use.

A notebook contains a set of **cells**. Each cell contains either **code** or **text** (written in a lightweight markup language called [Markdown](https://en.wikipedia.org/wiki/Markdown)). In the screenshot below, the very first cell of our Python 101 notebook contains a "text cell" and the second cell contains some Python code:

![](/software-carpentry/assets/jupyter_notebook_cells.png)

You can **add new cells** at the end of a notebook by clicking the **"+" button** in the second menu bar. To render the text you wrote in a "text cell" or execute the code in a "code cell", you have to **run the cell** by clicking on the **"play" symbol** (alternatively, you can use the keyboard shortcut `alt + ENTER`):

![](/software-carpentry/assets/jupyter_code.png)

By default, the type of cell is "code" but you can change it to "Markdown" if you intend to write notes in plain text. You can find the **type of the current cell** by looking at the dropdown, which also lets you change its type:

![](/software-carpentry/assets/jupyter_markdown.png)

**Tip:** in a "code cell", it is possible to run Bash commands by prepending the command with an exclamation mark, _e.g._, `!ls`.

That's it!

## Instructor notes

{% hint style='working' %}
These notes are mainly written for the instructors. Yet, they contain most (if not all) lines of code and important points taught during a workshop, which may be interesting if you want to remember how much you learnt during a workshop.
{% endhint %}

### :snake: in the shell

```
$ python3
>>>  # this is the python shell
>>>  # type ^D or exit() to quit
```

* Python is an interpreted language
* Run it from the shell

### Variables

```python
>>> x = 2  # integer
>>> is_dna = True  # boolean
>>> is_dna
True
>>> pi = 3.14  # float
>>> gnu = "A GNU is Not UNIX"  # string
>>> print(gnu)
"A GNU is Not UNIX"
>>> coordinates = [0.4, 1.2, 0.3]  # list
>>> coordinates = {'x': 0.4, 'y': 1.2, 'z': 0.3}  # dict
```

### Naming conventions

* Use `[A-Z]`, `[a-z]`, `[0-9]` & `_`
* Use snake case: `is_dna`
* :warning: a variable name with cannot start with a number
* :warning: you cannot use python keywords as names (e.g. `list`, `import`, etc.)

### Operations on variables

```python
>>> a = 4
>>> b = a + 1
>>> b
5
>>> a / 2  # integer division
2
>>> a ** 2  # power
4
>>> 'gc' * 4
'gcgcgcgc'
>>> seq = 'atgc'
>>> seq = seq + 'gc' * 4
>>> seq
'atgcgcgcgcgc'
```

**Exercise ideas:**

- Compute the area of a circle of 10 cm diameter using two variables `Pi` and `D` (the diameter)
- Generate a 100 nucleotides long poly-A sequence without typing the `A` key multiple times

### Working with lists

```python
>>> peptide = ['PRO', 'GLY', 'ALA']
>>> first_aa = peptide[0]
>>> first_aa
'PRO'
>>> second_peptide = ['ARG', 'ASN', 'ASP']
>>> peptide + second_peptide
['PRO', 'GLY', 'ALA', 'ARG', 'ASN', 'ASP']
>>> peptide.append('ARG')
>>> peptide
['PRO', 'GLY', 'ALA', 'ARG']
>>> peptide.pop()
'ARG'
>>> peptide
['PRO', 'GLY', 'ALA']
```

### More on lists

Lists can be nested!

```python
>>> crds = [[0.4, 1.2, 9.3], [0.5, 1.8, 9.1]]
>>> len(crds)
2
>>> len(crds[1])
3
>>> crds[0]
[0.4, 1.2, 9.3]
>>> crds[1][2]
9.1
```

### Loops

```
>>> peptide = ['PRO', 'GLY', 'ALA', 'ARG', 'ASN']
>>> for aa in peptide:
...     print(aa)
...
PRO
GLY
ALA
ARG
ASN
```

### Comparison operators

```python
>>> a = 5
>>> a == 5  # equal
True
>>> a != 2  # different than
True
>>> a > 5  # greater than
False
>>> a >= 5  # greater than or equal
True
>>> a < 5  # lower than
False
>>> a <= 5  # lower than or equal
True
```

### `while` loops

```python
>>> i = 1
>>> while i < 10:
...     print('^' * i)
...     i += 1  # identical to i = i + 1
^
^^
^^^
^^^^
^^^^^
^^^^^^
^^^^^^^
^^^^^^^^
^^^^^^^^^
```

### Control flow statements (1)

```python
>>> sequence = 'atgc'
>>> size = len(sequence)
>>> if size == 4:
...    print('Sequence length: OK')
Sequence length: OK
>>> if size == 4 and sequence == 'atgc':
...    print('Sequence match')
Sequence match
>>> if size == 6 or sequence == 'atgc':
...    print('Sequence match')
Sequence match
>>> if sequence == 'a' * len(sequence):
...    print('We have a Poly-A sequence')
... else:
...    print('Sequence is not a Poly-A')
```

### Control flow statements (2)

```python
>>> sequence = 'atgc'
>>> for nt in sequence:
...     if nt == 'a':
...         print('Found A')
...     elif nt == 't':
...         print('Found T')
...     else:
...         print('No A or T found')
Found A
Found T
No A or T found
No A or T found
```

**Exercise ideas:**

- Given the following sequence, calculate the ratio of each nucleotide type it contains:

```python
seq = 'ATGCTCGCGGCGCTAGCTACTAGCTAGCA'
```

- Given these crambine (alpha carbons) 10-first coordinates, calculate the peptide barycenter (mean coordinates):

```python
ca_trace = [  
    #     x,      y,     z
    [16.967, 12.784, 4.338],  # THR
    [13.856, 11.469, 6.066],  # THR
    [13.660, 10.707, 9.787],  # CYS
    [10.646, 8.991, 11.408],  # CYS
    [9.448, 9.034, 15.012],  # PRO
    [8.673, 5.314, 15.279],  # SER
    [8.912, 2.083, 13.258],  # ILE
    [5.145, 2.209, 12.453],  # VAL
    [5.598, 5.767, 11.082],  # ALA
    [8.496, 4.609, 8.837],  # ARG
]
```

### Working with files

```python
>>> f = open('./foo.fasta')
>>> for line in f:
...     print(line)
...
>foo

ATGCTCGCGGCGCTAGCTACTAGCTAGCA

>>> f.close()
>>> # alternative method: the with statement
>>> with open('./foo.fasta') as f:
...     lines = f.readlines()
>>> lines
['>foo\n', 'ATGCTCGCGGCGCTAGCTACTAGCTAGCA\n']
```

**Exercise ideas:**

- Download the crambine sequence in **fasta format** from the [PDB](http://www.rcsb.org/pdb/download/downloadFile.do?fileFormat=FASTA&compression=NO&structureId=1CRN). Save this file in your working directory and store the amino-acids sequence in a `seq` variable.

### Using modules

```python
>>> import math
>>> math.pi
3.141592653589793
>>> from math import pi
>>> pi
3.141592653589793
>>> from urllib import request
>>> url = 'http://www.rcsb.org/too/long/url'
>>> response = request.urlopen(url)
>>> for line in response.readlines():
...     print(line)
b'>1CRN:A|PDBID|CHAIN|SEQUENCE\n'
b'TTCCPSIVARSNFNVCRLPGTPEAICATYTGCIIIPGATCPGDYAN\n'
```

**Exercise ideas:**

- Re-implement your solution from the exercise 3.1 using the `urllib` module to download a fasta sequence from the PDB.

### Functions

Isolate repetitive tasks in fonctions:

```python
>>> def get_dna_complement(sequence):
...     complement = ''
...     for nt in sequence:
...         if nt == 'A':
...             complement += 'T'
...         elif nt == 'T':
...             complement += 'A'
...         elif nt == 'G':
...             complement += 'C'
...         elif nt == 'C':
...             complement += 'G'
...         else:
...             print("Unknown nucleotide:", nt)
...     return complement
>>> complement = get_dna_complement('ATGC')
>>> complement
'TACG'
```

### Variables scope

```python
>>> a = 10
>>> def foo():
...     a = 0
...     print("in foo:", a)
>>> foo()
in foo: 0
>>> print(a)
10
```