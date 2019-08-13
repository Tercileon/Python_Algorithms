|[Table of Contents](/00-Table-of-Contents.md)|
|---|

---

## Stacks
A stack is a data structure that is often likened to a stack of plates. 
If you have just washed a plate, you put it on top of the stack. When you need a plate, 
you take it off the top of the stack. 
So the last plate to be added to the stack will be the first to be removed from the stack. 
Thus, a stack is a last in, first out (LIFO) structure:

![](/Assets/plates.png)

The preceding figure depicts a stack of plates. Adding a plate to the pile is only possible by leaving that plate on top of the pile. To remove a plate from the pile of plates means to remove the plate that is on top of the pile.There are two primary operations that are done on stacks: push and pop. When an element is added to the top of the stack, it is pushed onto the stack. When an element is taken off the top of the stack, it is popped off the stack. Another operation which is used sometimes is peek, which makes it possible to see the element on the stack without popping it off.Stacks are used for a number of things. One very common usage for stacks is to keep track of the return address during function calls. Let's imagine that we have the following little program:

```python
def b():
    print('b')
    
def a():
    b()
    
a()
print("done");

```

When the program execution gets to the call to a(), it first pushes the address of the following instruction onto the stack, then jumps to a. Inside a, b() is called, but before that, the return address is pushed onto the stack. Once in b() and the function is done, the return address is popped off the stack, which takes us back to a(). When a has completed, the return address is popped off the stack, which takes us back to the print statement.

Stacks are actually also used to pass data between functions. Say you have the following function call somewhere in your code:

```python
somefunc(14, 'eggs', 'ham','spam')

```

What is going to happen is that 14, 'eggs', 'ham' and 'spam' will be pushed onto the stack, one at a time:

![](/Assets/Node0.png)

When the code jumps into the function, the values for a, b, c, d will be popped off the stack. The spam element will be popped off first and assigned to d, then "ham" will be assigned to c, and so on:

```python
def somefunc(a, b, c, d):
    print("function executed");
    
```

**Stack implementation**

Now let us study an implementation of a stack in Python. We start off by creating a node class, just as we did in the previous chapter with lists:

```python
class Node:
    def _init_(self, data = None):
        self.data = data
        self.next = None
```

This should be familiar to you by now: a node holds data and a reference to the next item in a list. We are going to implement a stack instead of a list, but the same principle of nodes linked together still applies.

Now let us look at the stack class. It starts off similar to a singly linked list. We need to know the node at the top of the stack. We would also like to keep track of the number of nodes in the stack. So we will add these fields to

```python
class stack:
    def _init_(self):
        self.top = None
        self.size = 0
        
```

**Push operation**

The push operation is used to add an element to the top of the stack. Here is an implementation:

```python
def push(self, data):
    node = Node(data)
    if self.top:
        node.next = self.top
        self.top = node
    else:
        self.top = node
    self.size += 1
```

In the following figure, there is no existing node after creating our new node. Thus self.top will point to this new node. The else part of the if statement guarantees that this happens:

![](/Assets/Node.png)

In a scenario where we have an existing stack, we move self.top so that it points to the newly created node. The newly created node must have its next pointer, pointing to the node that used to be the top node on the stack:

![](/Assets/Node2.png)


**Pop operation**

Now we need a pop method to remove the top element from the stack. As we do so, we need to return the topmost element as well. We will make the stack return None if there are no more elements:

```python
def pop(self):
    if self.top:
        data = self.top.data
        self.size -= 1
        if self.top.next:
            self.top = self.top.next
        else:
            self.top = None
        return data
    else:
        return None
```

The thing to pay attention to here is the inner if statement. If the top node has its next attribute pointing to another node, then we must set the top of the stack to now point to that node:

![](/Assets/Node3.png)

When there is only one node in the stack, the pop operation will proceed as follows:

![](/Assets/Node4.png)

Removing such a node results in self.top pointing to None:

![](/Assets/Node5.png)

**Peek**

As we said earlier, we could also add a peek method. This will just return the top of the stack without removing it from the stack, allowing us to look at the top element without changing the stack itself. This operation is very straightforward. If there is a top element, return its data, otherwise return None (so that the behavior of peek matches that of pop):

```python
def peek(self):
    if self.top
        return self.top.data
    else:
        return None
```

---

|[Next Topic](/15_Stack%20Implementation_Lesson.md)|
|---|
