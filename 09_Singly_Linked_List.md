|[Table of Contents](/00-Table-of-Contents.md)|
|---|

---

## Singly Linked List

**Objectives**

* detailed understanding on what is a singly linked list
* Understand how singly linked list are used
* Understand basic operations that can be performed on singly linked lists
* Perform basic operations on singly linked lists

---

**Pre-requirments**

Prior to this topic, you should have a basic understanding of: 

* Python 3
* OOP concepts
* Basic understanding of the purpose of singly linked lists

---

**Nodes**

Before we get into the details of what singly lists are, we must learn what nodes are. This is because nodes are the building blocks of a linked list. A node consists of two parts:

Data part - contains the data
Address part - this is pointer that points to location of the next node
In a singly linked list, each node’s address part contains the information about the location of the next node. This forms a series of chain or links. The first node of the linked list is kept track by the head pointer. The last node points to None.

Let us see the following diagram to understand this better:

![](/Assets/linklist.png)

Note: In the above figure, the last element 1 points to None. Even though these nodes are drawn contiguous to each other, in reality, they may or may not be in contiguous memory locations.

Check out this animation for the visualization of the working of a linked list.

Tip: Always try to draw these data structures to get a clear understanding.

How to create a Singly Linked List?
Creating classes
Firstly, you must create a node in order to create a singly linked list. To do this, we create a class Node with data and nextNode attributes. As discussed earlier, the data attribute will contain the data and the nextNode will simply point to the next node in the linked list. We will make the default value of nextNode to be None. You can use getter and setter methods to do this.

Now that the Node class is created, it is time to create the LinkedList class. This has only one attribute, head. By default, this will point to None. If the head points to None it means that the linked list is empty. To keep track of the number of nodes in the linked list, we can add a size attribute to the LinkedList class and default it to 0.

Inserting a Node
This is a method of the LinkedList class. Remember, to make the coding simple and efficient we will always add the new node to the beginning of the linked list. In other words, the head will always point to the most recently added node. If we add the new node to the end of the list, we need to do the extra work of finding the end of the list and then adding it. This is a wasteful operation. However, if you maintain another pointer, let’s call it the tail pointer such that it points to the last node, this can be done. You can insert a new node anywhere in the linked list. We have discussed the former approach i.e insertion at the beginning of the linked list.

Let’s say we need to add 7 to a linked list, we need to do the following steps:

Create a node object with 7 as the data and the next node pointing to head node
Point the head pointer to this new node
Finally, increment the size attribute by 1. It is always a good practice to return True if insertion was successful. This way the user knows what is happening.

Print Nodes
This is a method of the LinkedList class. To print the data present in all the nodes of the linked list, we need to traverse one node at a time and print each node’s data part.

---

**Coding a Singly Linked List**

```python

Class Node:
    def _init_(self, data, nextNode = None):
        self.data = data
        self.nextNode = nextNode
        
    def getData(self):
        return self.data
        
    def getNextNode(self):
        return self.nextNode
        
    def setNextNode(self, val):
        self.nextNode = val

 class LinkedList:
    def _init_(self, head = None):
        self.head = head
        self.size = 0
        
    def getSize(self):
        return self.size
        
    def addNode(self, data):
        newNode = Node(data, self.head)
        self.head = newNode
        self.size+=1
        return True
        
    def printNode(self):
        curr = self.head
        while curr:
            print(curr.data)
            curr = curr.getNextNode()

myList = LinkedList()
print("Inserting")
print(myList.addNode(5))
print(myList.addNode(15))
print(myList.addNode(25))
print("Printing")
myList.printNode()
print("Size")
print(myList.getSize)

```
---

**What are the advantages and disadvantages of Singly Linked Lists?**  

* **Advantages**

  * It’s a dynamic data structure in which insertion and deletion are simple as we don’t need to shift the elements. Just updating the next pointer will do the job for us.
  * Stack and Queue data structures can be easily implemented using linked lists.

* **Disadvantages**

  * Additional memory is used up by the next pointers.
  * Random access is not possible. You must traverse the linked list from the beginning to get to a particular node.

---

**Summary**

Throughout this topic we covered:
* Nodes
* What singly linked list are
* Some basic coding of a singly linked list
* Advantages of singly linked lists
* Disadvantages of singly linked lists

---

|[Next Topic](/10_Doubly_Linked_List.md)|
|---|
