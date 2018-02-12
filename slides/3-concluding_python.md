# Lab 4: Threads, Generators and pdb #

## We'll look at both the **threading** and **multiprocessing** modules and try some exercises ##

You can take a look at the **threading** and **mulitprocessing**
modules for the python standard library.
https://docs.python.org/3/library/threading.html           
https://docs.python.org/3/library/multiprocessing.html

### 1. First we'll take a look at the **threading** module

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

#### 1. Thread

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

t = Thread(target=foo, args=("test", "more_test"), kwargs={"c": "kw_test"})
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
Moving on...
So how do we know they're actually running? Let's create another function _goo_ that does nothing.

```Python
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

Will the execution wait while _goo_ sleeps or will _foo_ execute first and leave _goo_ behind?
Find out by executing.
- 5 seconds is too long to wait. Find out and implement how you can kill the thread after just 1 second.
- What if _join_ is not there? What will happen then?

#### 2. Communication among threads

The problems with threads in python are the same with threads in any
environment: Synchronization, Deadlocks, Race Conditions.

We won't deal with all of those here, as Deadlocks and Race Conditions
can be solved with an algorithmic approach, but Synchronization is one
thing which we'll see how to deal with in python3.

Consider a scenario of a Client-Server response type mechanism:
- There are k servers and each can serve at most m clients at a time. (In the general case it would be $m_1, m_2, ..., m_k$, one value for each server)
- Consider a fact that you want at most $n < km$ threads to be active at any given moment.
- You'd have  to keep track of which of the threads are active and assign them tasks as the client requests come in to the servers.

```Python
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

- **Write code to generate a list of clients with ids 1 - 100, which in turn each request the server with request_server method in a random order and at random times. Adapt the following code to implement random requests. You have to find out which server has the least load and you have to fill in all the required code.**

```Python
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
