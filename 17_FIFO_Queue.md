|[Table of Contents](/00-Table-of-Contents.md)|
|---|

---

## FIFO Queue
The python Queue class implements a basic first-in, first-out collection. 
Items can be added to the end of the container using put(), and removed from the head using get().

The constructor for a FIFO queue is as follows:

> class Queue.Queue(maxsize = 0)

The parameter maxsize is an integer used to limit the items that can be added into the queue.

Insertion will be blocked once the queue is full, until items are consumed.  The queue size is infinite if maxsize <= 0.

See the following example for how to use the FIFO queue:

```python
import Queue

q = Queue.Queue()

# put items at the end of the queue
for x in range(4):
    q.put("item-" + str(x))
    
# remove items from the head of the queue
while not q.empty():
    print q.get()
    
# the output
item-0
item-1
item-2
item-3

```

**Creating a FIFO Queue**

```python
// Initialize queue
Syntax: queue.Queue(maxsize)

// Insert Element
Syntax: Queue.put(data)

// Get And remove the element
Syntax: Queue.get()

import queue

# From class queue, Queue is created as an object
# Now L is Queue of a maximum capacity of 20
L = queue.Queue(maxsize = 20)

# Data is inserted into Queue using put()
# Data is inserted at the end
L.put(5)
L.put(9)
L.put(1)
L.put(7)

# get() takes data out from the Queue from the head of the Queue
print(L.get())
print(L.get())
print(L.get())
print(L.get())

Output:

5
9
1
7
```

---

|[Que DemoLab](/18_Queue_demo_lab.md)|
|---|
