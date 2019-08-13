|[Table of Contents](/00-Table-of-Contents.md)|
|---|

---

## CASE STUDY: SIMULATING A SUPERMARKET CHECKOUT LINE

In this case study, you develop a program to simulate supermarket checkout stations. To keep the program simple, some important factors found in a realistic supermarket situation have been omitted; you’re asked to add them back as part of the exercises.

**Request**

Write a program that allows the user to predict the behavior of a supermarket checkout line under various conditions.

**Analysis**

For the sake of simplicity, the following restrictions are imposed:

Image There is just one checkout line, staffed by one cashier.

Image Each customer has the same number of items to check out and requires the same processing time.

Image The probability that a new customer will arrive at the checkout does not vary over time.

The inputs to the simulation program are the following:

Image The total time, in abstract minutes, that the simulation is supposed to run.

Image The number of minutes required to serve an individual customer.

Image The probability that a new customer will arrive at the checkout line during the next minute. This probability should be a floating-point number greater than 0 and less than or equal to 1.

The program’s outputs are the total number of customers processed, the number of customers left in the line when the time runs out, and the average waiting time for a customer. Table 8.3 summarizes the inputs and outputs.

| Inputs | Range of Value for Inputs | Outputs |
|--------| :---: |--------|
|Total minutes| 0<=total <= 1000 | Total customers processed |
|Average minutes per customer| 0<average <= total | Customers left in line |
|Probability of a new arrival in the next minute| 0<probability <= 1| Average waiting time|

The User InterfaceThe following user interface for the system has been proposed:

```
Welcome the Market Simulator

Enter the total running time: 60
Enter the average time per customer: 3
Enter the probability of a new arrival: 0.25
TOTALS FOR THE CASHIER
Number of customers served: 16
Number of customers left in queue: 1
Average time customers spend
Waiting to be served: 2.38
```

---

**Classes and Responsibilities**

As far as classes and their overall responsibilities are concerned, the system is divided into a main function and several model classes. The main function is responsible for interacting with the user, validating the three input values, and communicating with the model. The design and implementation of this function require no comment, and the function’s code is not presented. The classes in the model are listed in the following table:

| Class | Responsibilities|
|--------|--------|
|MarketModel|A market model does the following:|
| |1. Runs the simulation|
| |2. Creates a cashier object|
| |3. Sends new customer objects to the cashier|
| |4. Maintains an abstract clock|
| |5. During each tick of the clock, tells the cashier to provide another unit of servie to a customer|
| Cashier | A cashier object does the following:|
| |1. Contains a queue of customers objects|
| |2. Adds new customer objects to this queue when directed to do so|
| |3. Removes customers from the queue in turn|
| |4. Gives the current customer a unit of service when directed to do so and releases the customer when the service has been completed|
| Customer| A customer object:|
| |1. Knows its arrival time and how much service it needs|
| |2. Knows when the cashier has provided enough service.  The class as a whole generates new customers when directed to do so according to the probability of a new customer arriving|
|LinkedQueue | Used by a cashier to represent a line of customers|

The relationships among these classes are shown in

![](/Assets/Linkedqueue1.png)

The overall design of the system is reflected in the collaboration diagram shown

![](/Assets/Linkedqueue2.png)

You can now design and implement each class in turn.

Because the checkout situation has been restricted, the design of the class MarketModel is fairly simple. The constructor does the following:

* Saves the inputs—probability of new arrival, length of simulation, and average time per customer.
* Creates the single cashier.

The only other method needed is runSimulation. This method runs the abstract clock that drives the checkout process. On each tick of the clock, the method does three things:

* Asks the Customer class to generate a new customer, which it may or may not do, depending on the probability of a new arrival and the output of a random number generator.
* If a new customer is generated, sends the new customer to the cashier.
* Tells the cashier to provide a unit of service to the current customer.

When the simulation ends, the runSimulation method returns the cashier’s results to the view. Here is the pseudocode for the method:

```python
for each minute of the simulation 
    ask the Customer class to generate a new customer
    if a customer is generated
        cashier.addCustomer(customer)
        cashier.serveCustomers(current time)
    return cashier's results
```

**Note:** The pseudocode algorithm asks the Customer class for an instance of itself. Because it is only probable that a customer will arrive at any given minute, occasionally a customer will not be generated. Rather than code the logic for making this choice at this level, you can bury it in a class method in the Customer class. From the model, the Customer class method generateCustomer receives the probability of a new customer arriving, the current time, and the average time needed per customer. The method uses this information to determine whether to create a customer and, if it does, how to initialize the customer. The method returns either the new Customer object or the value None. The syntax of running a class method is just like that of an instance method, except that the name to the left of the dot is the class’s name.

---

**Complete listing of the class MarketModel:**

```python
"""
File: marketmodel.py
"""

from cashier import Cashier
from customer import Customer

class MarketMode(object):

    def _init_(self, lengthOfSimulation, averageTimePerCus, probabilityOfNewArrival):
        self._probabilityOfNewArrival =\ probabilityOfNewArrival
        self._lengthOfSimulation = lengthOfSimulation
        self._averageTimePerCus = averageTimePerCus
        self._cashier = Cashier()
        
    def ruSimulation(self):
        """Run the clock for n ticks."""
        for currentTime in range(self._lengthOfSimulation):
            # Attemt to generate a new customer
            customer = Customer.generateCustomer(self._probabilityOfNewArrival, currentTime, self._averageTimePerCus)
            
            #send customer to cashier if successfully generated
            if customer != None
                self._cashier to provide another unit of service self._cashier.serveCustomers(currentTime)
                
    def _str_(self):
        return str(self._cashier)
        
```

A cashier is responsible for serving a queue of customers. During this process, the cashier tallies the customers served and the minutes they spend waiting in line. At the end of the simulation, the class’s __str__ method returns these totals as well as the number of customers remaining in the queue. The class has the following instance variables:

```
totalCustomerWaitTime
customerServed
queue
currentCustomer
```

The last variable holds the customer currently being processed.

To allow the market model to send a new customer to a cashier, the class implements the method addCustomer. This method expects a customer as a parameter and adds the customer to the cashier’s queue.

The method serveCustomers handles the cashier’s activity during one clock tick. The method expects the current time as a parameter and responds in one of several different ways, as listed in

|Condition|What It Means|Action to Perform|
|------------|-----------|----------|
|The current customer is None and the queue is empty| There are no customers to serve| Noen;just return |
|The current customer is None and the queue is empty| There is a customer waiting at the front of the queue| 1. Pop a customer and make it the current customer|
| | | 2. Ask it when it was instantiated, determine how long it has been waiting, and add that time to the total waiting time for all customers|
| | | 3. Increment the number of customers served|
| | | 4. Give the customer a unit of service and dismiss it if it is finished|
|The current customer is not None| Serve the current customer|Give the customer one unit of service and dismiss it if it is finished|

---

**Pseudocode for the method serveCustomers:**

```python
if currentCustomer is None:
    if queue is empty:
        return
    else:
        currentCustomer = queue.pop()
        totalCustomerWaitTime = totalCustomerWaitTime + currentTime - currentCustomer.arrivalTime()
        increment customerServed
        currentCustomer.serve()
        if currentCustomer.amountOfSeriveNeeded() == 0:
            currentCustomer = None

```

---

**Code for the Cashier class:**

```python
"""
File: cashier.py
"""

from linkedqueue import LinkedQueue

class Cashier(object):
    
    def _init_(self):
        self._totalCustomerWaitTime = 0
        self._customersServed = 0
        self._currentCustomer = None
        self._queue = LinkedQueue()
        
    def addCustomer(self, c):
        self._queue.add(c)
        
    def serveCustomers(self, currentTime):
        if self._currentCustomer is None:
            # No Customers yet
            if self._queue.isEmpty():
                return
            else:
                # Pop first waiting customer and tally results
                self._currentCustomer = self._queue.pop()
                self._totalCustomerWaitingTime += \ currentTime - \
                    self._currentCustomer.arrivalTime()
                self._customersServed += 1
                
            # Give a unit of service
            self._currentCustomer.serve()
            
            # If current customer is finished, send it away 
            if self._currentCustomer.amountOfServiceNeeded() == \ 
            0:
            self._currentCustomer = None
             
    def _str_(self):
        result = "TOTALS FOR THE CASHIER\n" + \
            "Number of customers served:     " +\
            str(self._customersServed)  +  "\n"
        if self._customersServed != 0:
        aveWaitTime = self._totalCustomerWaitTime /\
            self._customersServed
        result += "Number of customers left in queue: " \
            + str(len(self._queue)) + "\n" + \
                "Average time customers spend\n" + \
                "watiting to be served:          " \
                + "%5.2f" % aveWaitTime
    return result
```

The Customer class maintains a customer’s arrival time and the amount of service needed. The constructor initializes these with data provided by the market model. The instance methods include the following:

Image arrivalTime()—Returns the time at which the customer arrived at a cashier’s queue.

Image amountOfServiceNeeded()—Returns the number of service units left.

Image serve()—Decrements the number of service units by one.

The remaining method, generateCustomer, is a class method. It expects as arguments the probability of a new customer arriving, the current time, and the number of service units per customer. The method returns a new instance of Customer with the given time and service units, provided the probability is greater than or equal to a random number between 0 and 1. Otherwise, the method returns None, indicating that no customer was generated. The syntax for defining a class method in Python is the following:

```python
@classmethod
def <method name> (cls, <other parameters>):
    <statement>
```

---

**Code for the Customer class:**

```python
"""
File:  customer.py
"""

import random

class Customer(object):

    @classmethod
    def generateCustomer(cls, probabilityOfNewArrival, arrivalTime, averageTimePerCustomer):
        """Returns a Customer ofject if the probability of arrival is greater than or equal to a random number.
        otherwise, returns None, indicating no new customer."""
        
        if random.random() <= probabilityOfNewArrival:
            return Customer(arrivalTime, averageTimePerCustomer)
        else:
            return None
            
    def _init_((self, arrivalTime, serviceNeeded):
        self._arrivalTime = arrivalTime
        self._amountOfServiceNeeded = serviceNeeded
        
    def arrivalTime(self):
        return self._arrivalTime
        
    def amountOfServicNeeded (self):
        return self._arrivalTime
        
    def amountOfServiceNeeded(self):
        return self._amountOfServiceNeeded
        
    def serve(self):
        """Accepts a unit of service from the cashier."""
        self._amountOfServiceNeeded -= 1
```          

---

|[Queue Demo Lab 2](/19_Queue_Demo_lab_2.md)|
|---|
