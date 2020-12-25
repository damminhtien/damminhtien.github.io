---
title: Python concurrency
tags: python, programming
---

@Author: damminhtien :whale:

@LastUpdate: 25/12/2020

# Python concurrency
> ### Concurrent mechanism in Python (key features from Python Cookbook)

As we know, concurrency is the ability of different parts or units of a program, algorithm, or problem to be executed out-of-order or in partial order, without affecting the final outcome.

Concurrency is always the advanced mechanism in every programming languages. But, it is worth, by understanding this stuff, we can do a lot of things: multi-tasking,avoiding IO-bound, CPU-bound,...

This document includes some key features of concurrency, these implementations are written in Python.

Reference: [Python Cookbook: Recipes for Mastering Python 3](https://www.oreilly.com/library/view/python-cookbook/0596001673/)

## 0. The theories
### What is a Thread?

A thread is a path of execution within a process. A process can contain multiple threads. @[Geeks4Greeks](https://www.geeksforgeeks.org/thread-in-operating-system/)

### Concurrent vs Parallel

A system is said to be concurrent if it can support two or more actions in progress at the same time. A system is said to be parallel if it can support two or more actions executing simultaneously. The key concept and difference between these definitions is the phrase " @[takuti](https://takuti.me/note/parallel-vs-concurrent/)

### Concurrent Execution in Python

There are several differences ways to implement concurrent execution in Python: 
* [threading](https://docs.python.org/3/library/threading.html) — Thread-based (what we focus on this document)
* [multiprocessing](https://docs.python.org/3/library/multiprocessing.html) — Process-based
* [multiprocessing.shared_memory](https://docs.python.org/3/library/multiprocessing.shared_memory.html) — Provides shared memory for direct access across processes
* [The concurrent package](https://docs.python.org/3/library/concurrent.html)
* [concurrent.futures](https://docs.python.org/3/library/concurrent.futures.html) — Launching parallel tasks
* [subprocess](https://docs.python.org/3/library/subprocess.html) — Subprocess management
* [sched](https://docs.python.org/3/library/sched.html) — Event scheduler
* [queue](https://docs.python.org/3/library/queue.html) — A synchronized queue class

### GIL

The Python Global Interpreter Lock or GIL, in simple words, is a mutex (or a lock) that allows only one thread to hold the control of the Python interpreter.

This means that only one thread can be in a state of execution at any point in time. @[realpython](https://realpython.com/python-gil/)

## 1. The basics

### Start the Thread
The threading library can be used to execute any Python callable in its own thread. To do this, you create a Thread instance and supply the callable that you wish to execute
as a target.

```python
import time
from threading import Thread


def coundown(n):
    while n > 0:
        print(n)
        n -= 1
        time.sleep(0.5)


t1 = Thread(target=coundown, args=(1000000,))
t1.start()
t2 = Thread(target=coundown, args=(10,))
t2.start()
```

### Terminate the Thread
Due to a global interpreter lock (GIL), Python threads are restricted to an execution model that only allows one thread to execute in the interpreter at any given time. For this reason, Python threads should generally not be used for computationally intensive tasks where you are trying to achieve parallelism on multiple CPUs. They are much
better suited for I/O handling and handling concurrent execution in code that performs blocking operations (e.g., waiting for I/O, waiting for results from a database, etc.).

```python
import time
from threading import Thread


class CountdownTask:
    def __init__(self):
        self._running = True

    def terminate(self):
        self._running = False

    def run(self, n):
        while self._running and n > 0:
            print(n)
            n -= 1
            time.sleep(1)


c = CountdownTask()
t = Thread(target=c.run, args=(10,))
t.start()
time.sleep(5)
c.terminate()  # Signal termination
t.join()

time.sleep(5)
print('Main thread terminate')
```

### Thread's status
Event instances are similar to a “sticky” flag that allows threads to wait for something
to happen. Initially, an event is set to 0. If the event is unset and a thread waits on the
event, it will block (i.e., go to sleep) until the event gets set. A thread that sets the event
will wake up all of the threads that happen to be waiting (if any). If a thread waits on an
event that has already been set, it merely moves on, continuing to execute.

```python
from threading import Thread, Event
import time


# Code to execute in an independent thread
def countdown(n, started_evt):
    started_evt.set()
    print('Countdown starting')
    while n > 0:
        print('T-minus', n)
        n -= 1
        time.sleep(5)


# Create the event object that will be used to signal startup
started_evt = Event()
# Launch the thread and pass the startup event
print('Launching countdown')
t = Thread(target=countdown, args=(10, started_evt))
t.start()
# Wait for the thread to start
started_evt.wait()
print('Countdown is running')
```

### Threading condition
Event objects are best used for one-time events. That is, you create an event, threads wait for the event to be set, and once set, the Event is discarded. Although it is possible to clear an event using its clear() method, safely clearing an event and waiting for it to be set again is tricky to coordinate, and can lead to missed events, deadlock, or other
problems (in particular, you can’t guarantee that a request to clear an event after setting it will execute before a released thread cycles back to wait on the event again). If a thread is going to repeatedly signal an event over and over, you’re probably better off using a Condition object instead. For example, this code implements a periodic timer that other threads can monitor to see whenever the timer expires:

```python
class PeriodicTimer:
    def __init__(self, interval):
        self._interval = interval
        self._flag = 0
        self._cv = threading.Condition()

    def start(self):
        t = threading.Thread(target=self.run)
        t.daemon = True
        t.start()

    def run(self):
        '''
        Run the timer and notify waiting threads after each interval
        '''
        while True:
            time.sleep(self._interval)
            with self._cv:
                self._flag ^= 1
                self._cv.notify_all()

    def wait_for_tick(self):
        '''
        Wait for the next tick of the timer
        '''
        with self._cv:
            last_flag = self._flag
            while last_flag == self._flag:
                self._cv.wait()


ptimer = PeriodicTimer(5)
ptimer.start()


# Two threads that synchronize on the timer
def countdown(nticks):
    while nticks > 0:
        ptimer.wait_for_tick()
        print('T-minus', nticks)
        nticks -= 1


def countup(last):
    n = 0
    while n < last:
        ptimer.wait_for_tick()
        print('Counting', n)
        n += 1


threading.Thread(target=countdown, args=(10,)).start()
threading.Thread(target=countup, args=(5,)).start()
```

### Basic semaphore
A critical feature of Event objects is that they wake all waiting threads. If you are writing a program where you only want to wake up a single waiting thread, it is probably better to use a Semaphore or Condition object instead.

```python
import threading
import time


# Worker thread
def worker(n, sema):
    # Wait to be signaled
    sema.acquire()
    # Do some work
    print('Working', n)
    sema.release()


# Create some threads
sema = threading.Semaphore(0)
nworkers = 10
for n in range(nworkers):
    t = threading.Thread(target=worker, args=(n, sema,))
    t.start()
sema.release()
```

### Thread communication

Perhaps the safest way to send data from one thread to another is to use a Queue from the queue library. We create a Queue instance that is shared by the threads. Threads then use put() or get() operations to add or remove items from the queue.

When using queues, it can be somewhat tricky to coordinate the shutdown of the producer and consumer. A common solution to this problem is to rely on a special sentinel value, which when placed in the queue, causes consumers to terminate.

Thread communication with a queue is a one-way and nondeterministic process. In general, there is no way to know when the receiving thread has actually received a message and worked on it. However, Queue objects do provide some basic completion features, as illustrated by the task_done() and join() methods.

One caution with thread queues is that putting an item in a queue doesn’t make a copy of the item. Thus, communication actually involves passing an object reference between threads. If you are concerned about shared state, it may make sense to only pass im‐
mutable data structures (e.g., integers, strings, or tuples) or to make deep copies of the queued items. out_q.put(copy.deepcopy(data)).

```python
from queue import Queue
from threading import Thread
import random
import time


# Object that signals shutdown
_sentinel = object()


# A thread that produces data
def producer(out_q):
    while True:
        time.sleep(0.01)
        # Produce some data
        data = random.randint(0, 10)
        print('Produce data', data)
        out_q.put(data)
    # Put the sentinel on the queue to indicate completion
    out_q.put(_sentinel)


# A thread that consumes data
def consumer(in_q):
    while True:
        # Get some data
        data = in_q.get()
        print('Receive data', data)

        # Check for termination
        if data is _sentinel:
            in_q.put(_sentinel)
            break

        # Indicate completion
        in_q.task_done()


# Create the shared queue and launch both threads
q = Queue()
t1 = Thread(target=consumer, args=(q,))
t2 = Thread(target=producer, args=(q,))
t1.start()
t2.start()
# Wait for all produced items to be consumed
q.join()
```

Although queues are the most common thread communication mechanism, you can build your own data structures as long as you add the required locking and synchronization. The most common way to do this is to wrap your data structures with a condition variable. For example, here is how you might build a thread-safe priority queue.

```python
import heapq
import threading


class PriorityQueue:
    def __init__(self):
        self._queue = []
        self._count = 0
        self._cv = threading.Condition()

    def put(self, item, priority):
        with self._cv:
            heapq.heappush(self._queue, (-priority, self._count, item))
            self._count += 1
            self._cv.notify()

    def get(self):
        with self._cv:
            while len(self._queue) == 0:
                self._cv.wait()
            return heapq.heappop(self._queue)[-1]
```

### Locking Critical Sections

To make mutable objects safe to use by multiple threads, use Lock objects in the threading library, as shown here:

```python
import threading


class SharedCounter:
    # A counter object that can be shared by multiple threads.
    def __init__(self, initial_value=0):
        self._value = initial_value
        self._value_lock = threading.Lock()

    def incr(self, delta=1):
        # Increment the counter with locking
        with self._value_lock:
            self._value += delta

    def decr(self, delta=1):
        # Decrement the counter with locking
        with self._value_lock:
            self._value -= delta
```

### Deadlock Avoidance

In multithreaded programs, a common source of deadlock is due to threads that attempt to acquire multiple locks at once. For instance, if a thread acquires the first lock, but then blocks trying to acquire the second lock, that thread can potentially block the progress of other threads and make the program freeze. One solution to deadlock avoidance is to assign each lock in the program a unique number, and to enforce an ordering rule that only allows multiple locks to be acquired in ascending order. The key to this recipe lies in the first statement that sorts the locks according to object identifier. By sorting the locks, they always get acquired in a consistent order regardless of how the user might have provided them to acquire().

```python
import threading
from contextlib import contextmanager

_local = threading.local()


@contextmanager
def acquire(*locks):
    locks = sorted(locks, key=lambda x: id(x))

    acquired = getattr(_local, 'acquired', [])
    if acquired and max(id(lock) for lock in acquired) >= id(locks[0]):
        raise RuntimeError('Lock Order Violation')

    # Acquire all of the locks
    acquired.extend(locks)
    _local.acquired = acquired

    try:
        for lock in locks:
            lock.acquire()
        yield
    finally:
        # Release locks in reverse order of acquisition
        for lock in reversed(locks):
            lock.release()
        del acquired[-len(locks):]


x_lock = threading.Lock()
y_lock = threading.Lock()


def thread_1():
    while True:
        with acquire(x_lock, y_lock):
            print('Thread-1')


def thread_2():
    while True:
        with acquire(y_lock, x_lock):
            print('Thread-2')


t1 = threading.Thread(target=thread_1)
t1.daemon = True
t1.start()
t2 = threading.Thread(target=thread_2)
t2.daemon = True
t2.start()
```

