---
author:
- |
    Akshay Badola
date: January 2018
title: Introduction to Python
---

[Overview]{}

Python
======

Why Python?
-----------

[Why Python?]{}

[Because it’s easy!]{}

-   Python is easy!

-   No semicolons, no type specifications. No memory management.
    Everything’s handled internally.

-   Python can be fast by using existing libraries.\
    (C library) $->$ (Python Wrapper) $->$ (Call from Python). Simple!
    Simple to use but not to build ourselves, though some tools exist to
    help. [@swig; @autowig]

-   Python is powerful as it’s a general purpose programming language
    and a specialized tool for someone who doesn’t want to interface
    with the system.

    -   You can create threads and call system processes.

    -   File reading and writing is a snap!

    -   You can interface with the system libraries to leverage other
        tools to assist you.

    -   You can create automated tools all in python which can integrate
        easily with your code and help you monitor your algorithms, test
        and debug.

[Why Python?]{}

[Also because it’s versatile and Powerful]{}

-   Python is a scripted language so it’s easy to run and evaluate
    statements. No long compile times!

-   Python has what’s called *duck typing* and garbage collection via
    reference counting.

-   Python has developed a HUGE ecosystem. There are tonnes of
    libraries!

-   Python numpy interfaces with the BLAS and LAPACK libraries if they
    exist on your system so linear algebra is really fast.

-   There’s lots of example code out there for you if you get stuck,
    including Neural Networks, Statistical Models, Simulations, Machine
    Learning Models etc.

-   We’ll use *iPython*.

Introduction to Python
----------------------

[Introduction to Python]{}

[The Basics]{}

-   These are equivalent\

-   Functions are simple\

-   A lot of the syntax is C style\

[Introduction to Python]{}

[The Basics contd.]{}

-   A lot of the syntax is C style\

-   There are a few basic data types, but each type is wrapped\

-   

Operators and Strings
---------------------

[Introduction to Python]{}

[Operators and Strings]{}

-   With standard C style operators:

-   Strings can be specified with either a single or double quote

Elementary Data Structures Concepts
-----------------------------------

[Introduction to Python]{}

[Data Structures]{}

-   Multiline strings

-   The simplest data structure. They’re a bit like the strings.

[Introduction to Python]{}

[Data Structures contd.]{}

-   But the two can’t be mixed.

-   In fact, in most cases you can’t mix types. There’s no implicit type
    conversion. But if types can mix, they’re usually subtypes of a more
    general type. Like both Integer and Float are subtypes of Number,
    and Number has certain properties which allows them to be
    added/subtracted etc. together.

[Introduction to Python]{}

[Data Structures contd.]{}

-   Although explicit type conversions are allowed.

-   List indexing:

Interlude
---------

[Introduction to Python]{}

[Exercises!]{}

-   What will the following code print and why?

-   Scope:

Scope
-----

[Introduction to Python]{}

[Scope]{}

-   Scope contd.:

Lists
-----

[Introduction to Python]{}

[List Operations]{}

Lists are objects of type `iterator`. (Numpy) Arrays can also be
iterated.

-   You should lookup these common functions on lists yourself:\
    index, pop, append, copy, reverse, sort

-   Some more examples are given at this link
    <http://openbookproject.net/thinkcs/python/english3e/lists.html>

-   We’ll demonstrate some list comprehensions and move on to
    dictionaries, sets and numpy.

Dictionaries and Sets
---------------------

[Introduction to Python]{}

[Dictionaries and sets]{}

Dictionaries are unordered (key, value) pairs.\

[Introduction to Python]{}

[Dictionaries and Sets compared to Lists]{}

Dictionaries are much faster because they’re indexed.\

Classes
-------

[Introduction to Python]{}

[Very quickly classes!]{}

[Introduction to Python]{}

[Instantiating and Communicating among Classes]{}

[Introduction to Python]{}

[Instantiating and Communicating among Classes]{}

Modules and OS
--------------

[Introduction to Python]{}

[Modules, OS and file handling]{}

[Introduction to Python]{}

[*with* syntax]{}

-   *with* syntax is used with objects that support some automatic
    exception handling

-   The cleanup code like file closing, memory freeing (though not
    required because of python’s GC), foreign/C objects freeing etc. is
    performed automatically, and if an error occurs, it is safely
    thrown.

-   You can have your own function be compatible with the the *with*
    clause but we won’t go into that. Search online for it!

The Python environment
----------------------

### Anaconda

[Introduction to Python]{}

[Environment: anaconda, ipython and pip]{}

Anaconda

-   Download <https://www.anaconda.com/download/#linux>

-   Install <https://conda.io/docs/user-guide/install/index.html>

-   Set path before using.\
    \$$>$export PATH=`path_to_conda/bin:`\$PATH.

-   conda help

-   Anaconda ships with a lot of pre-compiled packages so you don’t have
    to maintain them.

### Pip

[Introduction to Python]{}

[pip]{}

pip: Python package management

-   apt-get install python3-pip. dnf install python3-pip. zypper install
    python3-pip

-   pip3 search $<$package\_name$>$. Searches packages at PyPI.

-   pip3 install. Installs packages.

-   pip3 freeze. Lists install packages.

-   pip3 install -U. Forces an upgrade

-   pip3 uninstall. Uninstalls packages

-   pip3 install –user. Installs in the user namespace.

-   As an exercise to get familiar with it, we’ll install the packages
    we’ll be using using pip

-   pip3 install –user -U numpy scipy matplotlib ipython scikit-learn
    scikit-image pillow

### iPython

[Introduction to Python]{}

[iPython!]{}

We also have iPython!

-   Start by opening up ipython. Type `ipython3` at the terminal.

-   help(something) shows help for it.

-   tab auto completes a variable (functions are also variables, sort
    of).

-   `Ctrl-{a,e,b,f}` go
    `{start-of-line, end-of-line, back-one-char, forward-one-char}`

-   `Alt-{b,f}` go `{back-one-word, forward-one-word}`

-   `Ctrl-{p,n,k,y}` do
    `{previous-command, next-command, kill-line (cut), yank (paste, not necessarily a line)}`

-   `Ctrl-{Space, w}` do `{set-mark, kill-region (can use C-y to yank)}`

-   `Ctrl-{r,s}` do `{search-command-backward, search-command-forward}`

-   `Alt-{d,\}` does `{delete-word, delete-horizontal-space}`

[Introduction to Python]{}

[more iPython!]{}

-   `%quickref` lists a whole lot of useful commands. You can check it
    out at leisure.

-   `%run` runs a python script from iPython.

-   `%paste` pastes text preserving formatting, from clipboard (requires
    tk installed in ubuntu).

-   `%timeit, %%timeit` time a single line and multiline commands.

-   `%pdb` turns ON/OFF automatic python debugger.

-   `lsmagic` lists all the available iPython macros (magics).

-   If you have a newer version of iPython, `automagic` will be on so
    you can just do `run ./myscript.py` instead of `%run ./myscript.py`.

Some Miscellaneous Useful Stuff
-------------------------------

[Some String Operations]{}

-   String is not really a list in python but it feels like it.

[Introduction to Python]{}

[Exercises! (again)]{}

-   Write a small lambda function that given a number (say 4) generates
    a list of tuples like so

-   -   Now instead of the second number simply being one greater than
    the previous one, have it be the output of a user supplied function.
    gives

-   How do you sort a list of tuples according to just the first number
    of each tuple? \[hint: look at the documentation of list.sort\]

-   Now, what’s the simplest (perhaps a pythonic) way to convert this
    list (or any list) of tuples to a dictionary?

[Introduction to Python]{}

[Exercises! (cond.)]{}

-   -   Let’s say I wanted to give the arguments parser a list to parse.
    Notice the `type=str`. That determines the type of the argument
    which is parsed. But there’s no inbuilt datatype list that it can
    parse. How can you parse it?

-   Create a class that simply keeps track of the number of instances it
    has, and prints the total number each time a new instance is
    created. \[hint: recall the difference between class variables and
    instance variables\]

[Introduction to Python]{}

[Exercises! (contd.)]{}

-   Just like `map`, `reduce` is a function that takes a list but it
    also takes an intial value as an argument, and instead of simply
    applying the function on each element of the list, it applies it
    along with the initial value and continues it through the list until
    the list is reduced to a single value.\
    Can you use it to `join` a list of lists into a single list?\

-   Write a complete program which takes a directory as argument, reads
    all the files in there with a ’.py’ extension and for each file,
    lists the following to stdout.

    1.  All the import modules with a fully qualified name, .e.g.,
        `from os import path` should be shown as `os.path`

    2.  All the classes in the files, with all the functions

    3.  All the functions which are not members of any class.

[Python (contd.)]{}

[Exercises! (contd.)]{}

-   Write a program that reads a CSV file which has `;` as the
    delimiter, `#` as comment and it takes the last two columns,
    lowercases the strings and writes it to another CSV file.

Summary {#summary .unnumbered}
=======

[References]{}
