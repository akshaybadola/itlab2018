# Lab 4: Threads, Generators and pdb #

## We'll look at both the **threading** and **multiprocessing** modules ##
## Then we'll try some exercises ##

You can take a look at the **threading** and **mulitprocessing**
modules for the python standard library.
https://docs.python.org/3/library/threading.html
https://docs.python.org/3/library/multiprocessing.html

### First we'll take a look at the **threading** module

The primary way to create a thread from the library is the **Thread** class

```Python
from threading import Thread
# or import threading.Thread
```

Python threads have locks, lifetimes, contexts, names and everything
else that you expect of a standard thread. They are threads in every
sense of the way. There are various functions in the **threading**
module which you can use to check the various properties of the
currently active threads. You can look at the **threading** library
reference to find them.

#### Thread

Python's Thread class requires a target function to run and you need to start it explicitly.

```Python
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

t = Thread(target=foo, args=("test", "more_test"), kwargs={'c': "kw_test"})
t.start()
t.join()
```

The above is a simple example of thread creation. To spawn multiple
threads for the same function we have to create and call them. The
following code does that.


```Python
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
