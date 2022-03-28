---
layout: lab
num: lab04
ready: true
desc: "Binary Search Tree"
assigned: 2022-02-03 9:00:00.00-8
due: 2022-02-10 22:00:00.00-8
---
<div markdown="1">

# Goals for this lab

By the time you have completed this lab, you should be able to

* Know how to navigate a binary tree data structure
* Implement recursive functions for binary trees
* Implement binary search tree functions

## Collaboration policy
This lab may be done solo or with a partner. By default we will assume that your collaboration choice is the same as lab03. However, if you are looking to change your choice from lab03, fill the partner form for lab04 by Feb 03 at 9am <https://forms.gle/5G1RLBSV3qNHrJww8>

If you are working with a partner, make sure both you and your partner are able to view the code on a shared screen. You may not work separately on the lab.

## Step by Step Instructions

## Step 1: Create a git repo and get the starter code

If you are working with a partner, select a pilot, log into the CSIL machines.

## Step 1a: Create a git repo, add your partner as collaborator

* Create a repo for this lab on the pilot's github account (just like you did in lab00): To do this, open a browser and navigate to [www.github.com](www.github.com). Log into the pilot's github account. From the drop down menu on the left, select our class organization and proceed to create a new repo. You may refer to the instructions in lab00. Follow this naming convention: If your github username is jgaucho and your partner's is alily, your should name your repo lab08_agaucho_alily (usernames appear in alphabetical order). Also you must set the visibity of your repo to be 'PRIVATE' when creating it. We will not repeat these instructions in subsequent labs.

* The pilot should add the navigator as a collaborator on github, and the navigator should accept the request to join the repo. See instructions in previous labs

## Step 1b: Get the starter code

Lab04: starter code <https://github.com/ucsb-cs24-w22/lab04_STARTER>

There are three required files to copy from the class account this week. Get them all at once:

Verify you got all the files and try to compile them as follows:
```
-bash-4.3$ ls
intbst.cpp  intbst.h  testbst.cpp
```
The first thing you should do is create a simple Makefile that compiles intbst.cpp and testbst.cpp.

A binary search tree class for integers, class IntBST is defined in intbst.h - please study this file for details of the class's features:

The constructor, destructor, insert method and pre-order print method are already implemented in intbst.cpp. Notice the insert method will return false to indicate an attempt to insert a duplicate value; otherwise it inserts the value and returns true.
In Step 2, you will implement the other two print methods, in-order and post-order. In Step 3 you will implement the sum, count and contains methods. In Step 4, you will implement the predecessor, successor, and remove methods. Step 4 will likely take you the most time BY FAR, so plan accordingly.
The binary tree node structure is defined in the private area. The only instance variable is a node pointer, to point at the root node of the tree or at 0 if the tree is empty.
Several utility functions are declared in the private area too. These functions can be recursive (by virtue of their Node* parameters), and the public methods may choose to use them or not. See how the destructor uses clear, for example, and the insert method uses the overloaded version of insert, each by passing the root pointer to the corresponding utility function. Also take note of the definition of getNodeFor, which will be useful in several of the functions you need to implement. Consider implementing this function immediately after the print functions, and think about where you can reuse it.

# Step 2: Implement in-order and post-order binary tree printing

You should be able to run testbst now (assuming you compiled it in Step 2):
```
-bash-4.3$ ./testbst
Choice of tests:
  0. all tests
  1. just printInOrder
  2. just printPostOrder
  3. just sum
  4. just count
  5. just contains
Enter choice:
0
BST:
  pre-order: 64 8 4 32 16 128 512 256
  in-order:
  post-order:
  sum: 0
  count: 0
  contains 64? Y
  contains 4? Y
  contains 16? Y
  contains 128? Y
  contains 17? N
  contains 512? Y
  . . .
Empty BST:
  pre-order:
  in-order:
  post-order:
  sum: 0
  count: 0
  contains 16? N

```
Note that just the pre-order print is complete (and the sum, count and contains methods aren't working either).

Use an editor (e.g., emacs) to make the following changes to intbst.cpp - do not change any of the other files.

Fix the comment at the top to show your name(s) and the date.
Scroll to the print functions (starting line 60). See how the public method just passes the root pointer to the private function in each case. Implement the private functions, printInOrder and printPostOrder.
Save, and then test your print implementations: compile and execute testbst again, choosing either all tests or just one of your print functions to test.
Here are the correct results (abbreviated to show just the print orders):

BST:

  pre-order: 64 8 4 32 16 128 512 256

  in-order: 4 8 16 32 64 128 256 512

  post-order: 4 16 32 8 256 512 128 64

By the way, you should be able to draw the tree now, both by tracing the order of the inserts, or by interpreting the three orders above. Take a minute to try that now on a piece of scratch paper since it may be very helpful when implementing the remaining functions.

# Step 3: Implement three more binary search tree functions

First: switch roles between pilot and navigator if you did not already do that.

You may do these tasks in any order. Check the results of each part as you complete it.

Implement the helper function for sum() - notice the public method just returns the result of the helper function. We suggest you use recursion to do so. Think about these questions before starting to code: What's the base case? What should be returned in the base case? What should be returned in the general (recursive) case?
Implement the helper function for count() - this is very similar to the sum() function.
Implement the public contains method, either recursively or iteratively - both are about the same level of difficulty in this case. If you decide to use recursion, you can use getNodeFor() in your implementation of contains(). You won't need this utility function to solve the problem iteratively. In either case, remember the tree is a binary search tree, and so your solution should run in O(log n) time.
Here are the results of all tests from our solution - you should verify that your results match:
```
BST:
  pre-order: 64 8 4 32 16 128 512 256
  in-order: 4 8 16 32 64 128 256 512
  post-order: 4 16 32 8 256 512 128 64
  sum: 1020
  count: 8
  contains 64? Y
  contains 4? Y
  contains 16? Y
  contains 128? Y
  contains 17? N
  contains 512? Y
  . . .
Empty BST:
  pre-order:
  in-order:
  post-order:
  sum: 0
  count: 0
  contains 16? N
```

Be aware, however, that more rigorous testing will be done when your work is submitted (a different program is used for testing your functions, some with random data).

# Step 4: Implement predecessor, successor, and remove

Your final task for this lab is to implement getPredecessor(), getSuccessor(), and remove(). The predecessor of a value is the next lowest value, while the successor is the next highest. Note that these functions should be implemented using the inherent structure of the binary tree, not by an exhaustive search for the next value. It will very likely be helpful to draw out the tree (the pre-order print can help you with this) when understanding how to implement getPredecessor() and getSuccessor(). If the element passed to the function is the first (for predecessor) or last (for successor) element in the tree, the function should return 0. It should also return 0 if the value is not present in the tree. Both of these functions will likely be harder to implement than any of the prior functions in this lab. However, correct implementations of getPredecessor() and getSuccessor look VERY similar, so you will likely be able to reuse a lot of your logic.

Finally, move on to remove(), which is likely the hardest algorithm you will be asked to implement this quarter. It is not excessively complicated in principle, but getting it completely right can take a while. Consider switching off pilot and navigator as you are debugging your implementation. You will probably find it helpful to use either getPredecessor() or getSuccessor() in remove(). You can also use remove() inside of itself, though it should NOT be a recursive function--the difference being that only one additional call of remove() should EVER occur. As with predecessors and successors, drawing the tree will be very helpful.

A correct implementation of all functions should produce the following output from testbst when selecting option 0:

```
BST:
  pre-order: 64 8 4 32 16 128 512 256
  in-order: 4 8 16 32 64 128 256 512
  post-order: 4 16 32 8 256 512 128 64
  sum: 1020
  count: 8
  contains 64? Y
  contains 4? Y
  contains 16? Y
  contains 128? Y
  contains 17? N
  contains 512? Y
  predecessor of 64 is: 32
  predecessor of 512 is: 256
  predecessor of 4 is: 0
  successor of 64 is: 128
  successor of 512 is: 0
  successor of 4 is: 8
  removing 4
  removing 64
  removing 128
  contains 64? N
  contains 4? N
  contains 16? Y
  contains 128? N
  contains 17? N
  contains 512? Y
  pre-order: 256 8 32 16 512
Empty BST:
  pre-order:
  in-order:
  post-order:
  sum: 0
  count: 0
  contains 16? N
```
# Step 5: Create a testbench in a file test_intbst.cpp

In a file named test_intbst.cpp, include code to test all the functions that you implemented in intbst.cpp. Make sure that this file is compilable.

# Step 6: Submit your revised intbst.cpp, test_intbst.cpp and intbst.h

You are allowed to modify intbst.h, though you should not need to, so submit both intbst.cpp and intbst.h to Gradescope for a grade out of 100. 
# Optional Extra Challenge

AFTER you have completed the main lab, you may modify it for extra credit by converting your BST to a generic data structure. For convenience, we will not change any of the file or data structure names, but your structure should be useable as IntBST<T> where T is a type that can be compared with <, >, etc. This could include double, char, or any other basic type. There is a separate Gradescope submission portal for this extra credit assignment. Make sure to have a full-credit submission on the main assignment's Gradescope before working on this part.

Note that you should implement a generic type in intbst.cpp and include it in your header file as #include "intbst.cpp".
Submit files: intbst.h and intbst.cpp

</div>
