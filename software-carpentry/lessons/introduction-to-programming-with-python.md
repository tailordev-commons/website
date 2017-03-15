# Introduction to programming with Python

{% hint style='info' %}
You can find the Software Carpentry lesson at: https://swcarpentry.github.io/python-novice-inflammation/. Nonetheless, we believe **the SC lesson does not target complete beginners** to programming. That is why we do not use its content and we have developed our own materials.
{% endhint %}

On this page, you will find:

<!-- toc -->

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
- Generate a 100 nucleotides long poly-A sequence without typing the `A` key multiple times.

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

## Variables scope

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