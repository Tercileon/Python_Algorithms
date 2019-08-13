|[Table of Contents](/00-Table-of-Contents.md)|
|---|

---

## Doubly Linked List

**Objectives**

* Detailed understanding on what is a doubly linked list
* Understand how to create doubly linked lists
* Understand how to print all the nodes in a list

---
### Creating a Double Linked List

**Python program to create and display a doubly linked list.**

In this program, we will create a doubly linked list and print all the nodes present in the list.

Doubly Linked List is a variation of the linked list. The linked list is a linear data structure which can be described as the collection of nodes. Nodes are connected through pointers. Each node contains two fields: data and pointer to the next field. The first node of the linked list is called the head, and the last node of the list is called the tail of the list.

One of the limitations of the singly linked list is that it can be traversed in only one direction that is forward. The doubly linked list has overcome this limitation by providing an additional pointer that points to the previous node. With the help of the previous pointer, the doubly linked list can be traversed in a backward direction thus making insertion and deletion operation easier to perform. So, a typical node in the doubly linked list consists of three fields:

Data represents the data value stored in the node.
Previous represents a pointer that points to the previous node.
Next represents a pointer that points to the next node in the list.


![](/Assets/null.png)

The above picture represents a doubly linked list in which each node has two pointers to point to previous and next node respectively. Here, node 1 represents the head of the list. The previous pointer of the head node will always point to NULL. Next pointer of node one will point to node 2. Node 5 represents the tail of the list whose previous pointer will point to node 4, and the next will point to NULL.

---

**Algorithm:**

Define a Node class which represents a node in the list. It will have three properties: 
* **data**
* **previous** which will point to the previous node
* **next** which will point to the next node.

Define another class for creating a doubly linked list, and it has two nodes: head and tail. 

Initially, head and tail will point to null.

```
addNode() will add node to the list:
```

It first checks whether the head is null, then it will insert the node as the head.
Both head and tail will point to a newly added node.
Head's previous pointer will point to null and tail's next pointer will point to null.
If the head is not null, the new node will be inserted at the end of the list 
such that new node's previous pointer will point to tail.
The new node will become the new tail. Tail's next pointer will point to null.

a. display() will show all the nodes present in the list.

Define a new node 'current' that will point to the head.
Print current.data till current points to null.
Current will point to the next node in the list in each iteration.

---

**Program**

```python

#Represent a node of doubly linked list

class Node:
    def _init_(self, data):
    self.previous = None;
    self.next = None;
    
class DoublyLinkedList:

    # Represent the head and tail of the doubly linked list
    
    def_init_(self):
        self.head = None;
        self.tail = None;
        
    # If list is empty
    if(self.head == None):
        # Both head and tail will point to newNode
        self.head = self.tail = newNode;
        # head's previous will point to None
        self.head.previous = None
        # tail's next will pint to None, as it is the last node of the list
        self.tail.next = None;
        
    else:
        # newNode will be added after tail such that tail's next will point to newNode
        self.tail.next = newNode;
        # newNode's previous will point to tail
        newNode.previous = self.tail;
        # newNode will become new tail
        self.tail = newNode;
        # As it is last node, tail's next will point to None
        self.tail.next = None;
        
    # display() will print out the nodes of the list
    def display(self):
        # Node current will point to head
        current = self.head;
        if(self.head == None):
            print("list is empty");
            return;
        print("Nodes of doubly linked list: ");
        while(current != None):
            # Prints each node by incrementing pointer.
            print(current.data);
            current = current.next;
            
    dList = DoublyLinkedList();
    # Add nodes to the list
    dList.addNode(1);
    dList.addNode(2);
    dList.addNode(3);
    dList.addNode(4);
    dList.addNode(5);
   
    # Displays the nodes present in the list
    dList.display();
    
```

---

**Output:**
Nodes of doubly linked list: 
1 2 3 4 5

---

|[Next Topic](/11_Linked_List_Demo.md)|
|---|
