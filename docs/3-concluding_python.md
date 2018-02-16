# Threads, Generators and pdb #

## We'll take a look at the **threading** and **pdb** and try some exercises ##

You can take a look at the **threading** module for the python standard library.
<https://docs.python.org/3/library/threading.html>


### 1. First we'll take a look at the **threading** module

The primary way to create a thread from the library is the **Thread** class

```python
from threading import Thread
# or import threading.Thread
```

Python threads have locks, lifetimes, contexts, names and everything else that you expect of a standard thread. They are
threads in every sense of the way. There are various functions in the **threading** module which you can use to check
the various properties of the currently active threads. You can look at the **threading** library reference to find
them.

#### 1. Thread

Python's Thread class requires a target function to run and you need to start it explicitly.

```python
from threading import Thread

def foo(a=None, b=None, c=None):
    if not a and not b and not c:
        print("fooing")

    if a:
        print(a)
    if b:
        print(b)
    if c:
        print(c)
    if not a and not b and not c:
        print("fooing")

t = Thread(target=foo, args=("test", "more_test"), kwargs={"c": "kw_test"})
t.start()
t.join()
```

The above is a simple example of thread creation. To spawn multiple threads for the same function we have to create and
call them. The following code does that.


```python
from threading import Thread

def foo(a=None, b=None, c=None):
    if not a and not b and not c:
        print("fooing")
    if a:
        print(a)
    if b:
        print(b)
    if c:
        print(c)


threads = []
threads.append(Thread(target=foo))
threads.append(Thread(target=foo, args=("test")))
threads.append(Thread(target=foo, args=("test", "more_test")))
threads.append(
    Thread(target=foo, args=("test", "more_test"), kwargs={'c': "kw_test"}))

for t in threads:
    t.start()
    t.join()
```
Moving on... So how do we know they're actually running? Let's create another function _goo_ that does nothing.

```python
from time import sleep

def goo():
    # sleeps for a while
	sleep(5)
	# and then prints "gooing"
	print("gooing")

# goo is at the head of the threads list
threads = []
threads.append(Thread(target=goo))
threads.append(Thread(target=foo))


for t in threads:
    t.start()
for t in threads:
    t.join()
```

Will the execution wait while _goo_ sleeps or will _foo_ execute first and leave _goo_ behind?  Find out by executing.
- 5 seconds is too long to wait. Find out and implement how you can kill the thread after just 1 second.
- What if _join_ is not there? What will happen then?

#### 2. Communication among threads

The problems with threads in python are the same with threads in any environment: Synchronization, Deadlocks, Race
Conditions.

We won't deal with all of those here, as Deadlocks and Race Conditions can be solved with an algorithmic approach, but
Synchronization is one thing which we'll see how to deal with in python3.

Consider a scenario of a Client-Server response type mechanism:
- There are k servers and each can serve at most m clients at a time. (In the general case it would be $$m_1, m_2, ..., m_k$$, one value for each server)
- Consider a fact that you want at most $$n < km$$ threads to be active at any given moment.
- You'd have  to keep track of which of the threads are active and assign them tasks as the client requests come in to the servers.

```python
class Server:
    def __init__(self, max):
        self.__max_requests = max
        self.__current_requests = 0

    def request(self):
        if self.__current_requests + 1 < self.__max_requests:
            self.__current_requests += 1
            self.handle_request()
            return 0
        else:
            print("DENIED")
            return 1

    def handle_request(self, client):
        print("handling request for " + client.id)
        sleep(2)


class Client:
    def __init__(self, id):
        self.id = id

    def request_server(self, server_id):
        servers[server_id].request()
```

- **Write code to generate a list of clients with ids 1 - 100, which in turn each request the server with request_server
  method in a random order and at random times. Adapt the following code to implement random requests. You have to find
  out which server has the least load and you have to fill in all the required code.**

```python
# We want to have 5 servers, each of which can handle 5 requests at a time
# We have 100 clients, who each request randomly, and they're handled in FCFS manner

import time, random

## Make 5 servers and 100 clients

l = list(range(100))
random.shuffle(l)

for i in range(1000):
    ## cycle through the list and at the end of the list shuffle again
    client.request_server("server with least load")
```

- **Which problems will you face and how can you solve them?**

### 2. pdb: The Python Debugger

A debugger can be a program or a module which inspects the code as it runs and keeps track of the function calls and the
variables present. Debugging in python is done by breaking into the code at runtime with pdb.

```python
import pdb

pdb.run('foo()')
```
For scripts you can attach pdb to the python process by invoking the python command with `-m` switch.

```Bash
python3 -m pdb myscript.py
```

You can break into the code where you know the error is going to occur by using `pdb.set_trace()`

Inside the python debugger if an error occurs, you'll have an access to a debugging console.

```python
(Pdb) help
Documented commands (type help <topic>):
========================================
EOF    c          d        h         list      q        rv       undisplay
a      cl         debug    help      ll        quit     s        unt      
alias  clear      disable  ignore    longlist  r        source   until    
args   commands   display  interact  n         restart  step     up       
b      condition  down     j         next      return   tbreak   w        
break  cont       enable   jump      p         retval   u        whatis   
bt     continue   exit     l         pp        run      unalias  where    

Miscellaneous help topics:
==========================
exec  pdb

(Pdb) help h
h(elp)
        Without argument, print the list of available commands.
        With a command name as argument, print help about that command.
        "help pdb" shows the full pdb documentation.
        "help exec" gives help on the ! command.

(Pdb) help d
d(own) [count]
        Move the current frame count (default one) levels down in the
        stack trace (to a newer frame).

```

Above are the list of commands available to you in the debugger and you can seek further help on the manner as indicated above.

Generally the things you'll do is:
- Inspect the value of a variable.
  That you can do by simply typing the name of the variable at the prompt. Or using a `print(var)`.
- Evaluate an expression:
  You can do things like perform any expression w.r.t. to any variables present in that scope.
  You can call a function if it exists in the current scope.
  You can of course always print the current variables in scope  at any interpreter with the `dir()` function and use its output.
- You can go up and down in the calling stack by using `u` and `d` commands.
- You can print the source at the current scope with `l`.
- You can continue execution with `c` or restart with `r`.

Generally with small code i.e. below a 1000 LOC, it isn't usually that difficult to debug, but if your codebase grows
above that, you'll need to learn how to use  the debugger.

### 3. Generators and generator expressions
(Some part of this section is borrowed from https://wiki.python.org/moin/Generators)

"Generator functions allow you to declare a function that behaves like an iterator, i.e. it can be used in a for loop."
What it means, is that usually when you speak of an **iterator**, you're iterating over a structure. But what if you
were looping over an infinite structure? What if you want to iterate over the same structure but in a random manner?
What if you wanted to create a sequence instead of iterating over a fixed sequence?

For all these purposes, you have to use the **iterator** pattern.  You can make any class _iterable_ by adding two
functions to it: `__iter__` and `__next__`.

Consider the following code
```python
# Build and return a list
def firstn(n):
    num, nums = 0, []
    while num < n:
        nums.append(num)
        num += 1
    return nums

sum_of_first_n = sum(firstn(1000000))
```

Why doesn't this stupid thing display math?

$$ m_1, m_2, m_3, ... , m_n $$

ugh ugh 

\$$ m_1, m_2, m_3, ... , m_n $$

mugh mugh 

\$\$ m_1, m_2, m_3, ... , m_n $$

Crappy crap.

The above funtion definition simply generates a list till $$n$$. To sum up such a list, such a list will first have to
exist and then be summed up. You can also realize that the list doesn't really have to exist to compute the sum, nor to
use the values of the list in any other scenario. The only condition is that the numbers must be produced in
sequence. Such a sequence is encapsulated in the _iterable_ pattern.

```python
# Using the generator pattern (an iterable)
class firstn(object):
    def __init__(self, n):
        self.n = n
        self.num, self.nums = 0, []

    def __iter__(self):
        return self

    def __next__(self):
        if self.num < self.n:
            cur, self.num = self.num, self.num+1
            return cur
        else:
            raise StopIteration()

sum_of_first_n = sum(firstn(1000000))
```

The above code implements the two required functions and now the the type **firstn** can be looped over, as only that is
required for a loop to run. However, the code above can be simplified significantly as for many situations a lot of the
tasks are similar. For that we have **generators**. The below code accomplishes the same task as the above one:

```python
# a generator that yields items instead of returning a list
def firstn(n):
    num = 0
    while num < n:
        yield(num)
        num += 1

sum_of_first_n = sum(firstn(1000000))
```

"The performance improvement from the use of generators is the result of the lazy (on demand) generation of values,
which translates to lower memory usage. Furthermore, we do not need to wait until all the elements have been generated
before we start to use them. This is similar to the benefits provided by iterators, but the generator makes building
iterators easy."

Basically the generator object is now producing the numbers on demand instead of from a fixed object. The key part in
the generator is the `yield()` method which is equivalent to the `__next__` method of the _iterator_.

- **Write a generator function which generates an infinite sequence of random numbers between two given numbers.**
  **How will you use it? When will such a sequence stop?**

Generators are often used for batching as you need to loop over the batches of data infinitely (or until you get the
required result). In a generator you can shuffle the data at each iteration or at the end of the entire set of data, and
do modifications like rotate images or switch the color channels.

### Advanced exercise
- **Write a generator which takes a set of images and crops random fixed sized patches from a random subset, normalizes
  them (subtracts by the mean and divides by the standard deviation) and returns it.**

## Nuances of Threading in Python ##

So far we've used the **threading** library in python, which provides
light weight concurrency. However, there would be issues with running
multiple threads on the Python interpreter as it is not
thread-safe. <https://docs.python.org/3/c-api/init.html#thread-state-and-the-global-interpreter-lock>

Threads created 
