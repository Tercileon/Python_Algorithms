|[Table of Contents](/00-Table-of-Contents.md)|
|---|

---

## Practice Labs

---

**Exercise 1**

* Write a tester program that counts and displays the number of iterations of the following loop:

```python

while problemSize > 0:
    problemSize = problemSize // 2

```

* Run the program you created in Exercise 1 using problem sizes, of 1000, 2000, 4000, 10,000, and 100,000.  As the problem size doubles or increases by a factor of 10.  
**What happens to the number iterations?**

* The difference between the results of two calls of the functions time.time() is an elapsed time. Because the operating system might use the CPU for part of this time, the elapsed time might not reflect the actual time that a Python code segment uses the CPU. Browse the Python documention for an alternative way of recording the processing time, and describe how this would be done.

---

**Exercises 2**

* Suppose that a list contains the values 20, 44, 48, 55, 62, 66, 74, 88, 93, 99 at index positions 0 through 9.  Trace the values of the variables **left, right,** and **midpoint** in a binary search of this list for the target value 90.  Repeat for the target value 44. 

* The method that's usually used to look up an entry in a phone book is not exactly the same as a binary search because, when a phone book, you don't always go to the midpoint of the sublist being searched.  Instead, you estimate the position of the target based on the alphabetical position of the first letter of the person's last name. For example, when you are looking up a number for "Smith," you look toward the middle of the second half of the phone book first, instead of in the middle of the entire book.  Suggest a modification of the binary search algorithm that emulates this strategy for a list of names.  Is it computational complexity any better than that of the standard binary search?

---

**Exercises** 

* Describe the strategy of quicksort and explain why it can reduce the time complexity of sorting from O(*n*<sup>2</sup>) to O(*n* log *n*).

* Why is quicksort not O(*n* log *n*) in all cases? Describe the worst-case situation for quicksort and give a list of 10 integers, 1- 10, that would produce this behavior.

* The **partition** operation in quicksort chooses the item at the midpoint as the pivot.  Describe two other strategies for selecting a pivot value.

* Sandra has a bright idea: when the length of a sublist in quicksort is less than a certain number - say, 30 elements - run an insertion sort to process that sublist.  
**Explain why this is a bright idea.**

* Why is merge sort an O(*n* log *n*) algorithm in the worst case?

---

|[Next Topic](/06_Searching_Algorithms.md)|
|---|
