|[Table of Contents](/00-Table-of-Contents.md)|
|---|

---

## CASE STUDY: AN EMERGENCY ROOM SCHEDULER

As anyone who has been to a busy hospital emergency room knows, people must wait for service. Although everyone might appear to be waiting in the same place, they are actually in separate groups and scheduled according to the seriousness of their condition. This case study develops a program that performs this scheduling with a priority queue.

**Request**

Write a program that allows a supervisor to schedule treatments for patients coming into a hospital’s emergency room. Assume that, because some patients are in more critical condition than others, patients are not treated on a strictly first-come, first-served basis, but are assigned a priority when admitted. Patients with a high priority receive attention before those with a lower priority.

**Analysis**

Patients come into the emergency room in one of three conditions. In order of priority, the conditions are ranked as follows:

* Critical
* Serious
* Fair

When the user selects the Schedule option, the program allows the user to enter a patient’s name and condition, and the patient is placed in line for treatment according to the severity of his condition. When the user selects the Treat Next Patient option, the program removes and displays the patient first in line with the most serious condition. When the user selects the Treat All Patients option, the program removes and displays all patients in order from patient to serve first to patient to serve last.

Each command button produces an appropriate message in the output area. This Table lists the interface’s responses to the commands.

|User Command|Program Response|
|------------|----------------|
|Schedule|Prompts the user for the patient's name and condition, and then prints {patient name} is added to the {condition} list|
|Treat Next Patient|Prints{patient name} is being treated|
|Treat All Patients|Prints{patient name} is being treated....Prints {patent name} is being treated|

---
    
Here is an interaction with the terminal-based interface:

```python
Main Menu
    1 Schedule a patient
    2 Treat the next patient
    3 Treat all patients
    4 Exit the program
  
Enter a number [1-4]: 1
  
Enter the patient's name: Larry
Patient's condition:
    1 Critical
    2 Serious
    3 Fair
  
Enter a number [1-3]: 1
Larry is added to the critical list.

Main menu
      1 Schedule a patient
      2 Treat the next patient
      3 Treat all patients
      4 Exit the program
      
 Enter a number [1-4]: 3
 
 Larry/ critical is being treated.
 Steve/ serious is being treated.
 Laura/ fair is being treated.
 No patients available to treat.
 ```
 
**Classes**
The application consists of a view class, called ERView, and a set of model classes. The view class interacts with the user and runs methods with the model. The class ERModel maintains a priority queue of patients. The class Patient represents patients, and the class Condition represents the three possible conditions. The relationships among the classes are shown in the next Figure

![](/Assets/Condition1.png)

**Design and Implementation**

The Patient and Condition classes maintain a patient’s name and condition. You can compare (according to their conditions) and view them as strings. Here is the code for these two classes:

```python
class Condition(object):

    def _init_(self, rank):
        self._rank = rank
        
    def _ge_(self, other):
        """Used for comparison,"""
        return self._rank >= other._rank
        
    def _str_(self):
        if    self._rank == 1: return "critical"
        elif self._rank == 2:  return "serious"
        else:                  return "fair"
        
class Patient(object)

    def _init_(self, name, condition):
        self._name = name
        self._condition = condition
        
    def _ge_(self, other):
        """Used for comparisons."""
        return self._conditions >= other._conditions
        
    def _str_(self):
        return self._name + " /" + str(self._condition)
        
 ```

The class ERView uses a typical menu-driven loop. You structure the code using several helper methods. Here is a complete listing:

```python
"""
File: erapp.py
The view for an emergency room scheduler.
"""

from model import ERModel, Patient, Condition

class ERView(object):
    """ The view class for the ER application"""
    
    def _init_(self, model):
        self._model = model
        
    def run(self):
        """Menu-driven comand loop for the app."""
        
        menu = "Main menu\n" + \
            " 1 Schedule a patient\n" + \
            " 2 Treat the next patient\n" + \
            " 3 Treat all patients\n" \
            " 4 Exit the program\n"
        while True:
            command = self._getCommand(4, menu)
            if   command == 1:  self._schedule()
            elif command == 2:  self._treatNext()
            elif command == 3:  self._treatAll()
            else: break
            
    def treatNext(self):
        """Treats one patient if there is one."""
        if self.model.isEmpty():
            print("No patients available to treat")
        else:
            patient = self.model.treatNext()
            print(patient, "is being treated.")

    def treatAll(self):
        """ Treats all the remaining patients."""
        if self.model.isEmpty():
            print("No patients available to treat.")
        else:
            while not self.model.isEmpty():
                self.treatNext()
                
    def _schedule(self):
        """Obtains patient info and schedules patient."""
        name = input("\nEnter the patient's name:  ")
        condition = self._getCondition()
        self._model.schedule(Patient(name, condition))
        print(name, "is added to the", condition, "list\n")
        
    def _getCondition(self):
        """Obtains condition info."""
        menu = "Patient's condition:\n" + \
            " 1 Critical\n" + \
            " 2 Serious\n" + \
            " 3 Fair\n"
        number = self._getCommand(3, menu)
        return Condition(number)
        
    def_getCommand(self._getCommand(3, menu)
        """Obtains and returns a command number."""
        
        prompt = "Enter a number [1-" + str(high) + "]: "
        commandRange = list(map(str, range(1, high + 1)))
        error = "Error, number must be 1 to " + str(high)
        while True:
            print (menu)
            command = input(prompt)
            if command in comandRange:
                return int(command)
            else:
                print(error)
                
# Main function to start up the application 

    def main():
        model = ERModel()
        view = ERView(model)
        view.run()
        
    if _name_ == "_main_":
        main()
```

The class ERModel uses a priority queue to schedule the patients. Its implementation is left as a programming project for you.

**STUDENT PERFORMANCE LAB:** Queue Lab1

* Complete the emergency room scheduler application as described in the case study.

---

|[Queue Lab1](/20_Queue_Perf_Lab.md)|
|---|
