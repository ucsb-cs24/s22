---
layout: lab
num: lab04
ready: true
desc: "Binary Search Tree"
assigned: 2022-04-27 15:00:00.00-8
due: 2022-05-04 23:59:00.00-8
---
<div markdown="1">

# Goals for this lab

By the time you have completed this lab, you should be able to

* Know how to navigate a binary tree data structure
* Implement recursive functions for binary trees
* Implement binary search tree functions

## Collaboration policy
This lab may be done with a partner or solo. You can choose to work with the same partner from previous labs, form a new partnership, or ask the TAs to assign you a partner. However, you must fill out this form to announce your decision if you haven’t already for lab04: <https://forms.gle/DBh8F7dXcUqP6nPA7>
Although you may partner with the same partner as before, we strongly encourage you to work with someone new this time!

If you have identified a partner in your section who has also agreed to work with you or if you decide to work solo, you can begin working on the lab right after submitting the form.

However, if you are requesting for the TAs to assign a partner to you, you must wait until your section time on Thursday to hear about the assignment. Please respond to any communication from TAs or your partners quickly! Not responding to your partner by more than a day will lead to a 30% deduction in your grade.

If you missed the deadline, you must still fill the form before you begin working on this lab to get credit for the lab.

If you are working with a partner, make sure both you and your partner are able to view the code on a shared screen. You may not work separately on the lab.

## Academic Integrity
All work submitted for this lab should be your own and your partners. If you are using any hints from a previous offering of this course that was posted publicly by a CS24 instructor, you must cite your source.

## Step by Step Instructions

## Step 0: Create a git repo and get the starter code
Refer to lab01 for instructions on how to set up a GitHub repository and pull the starter code for this lab. Here is the link for this lab's starter code: <https://github.com/ucsb-cs24-s22/STARTER-lab04>
If you are working in pairs, only one partner needs to create the Repository, but make sure to add the other partner as a collaborator.

## Step 0a: The starter code

There are three required files to copy from the class account this week. After pulling the starter code, you should be able to type the command ```ls``` and see the following files in your directory.
```
-bash-4.3$ ls
intbst.cpp  intbst.h  testbst.cpp
```
The first thing you should do is create a simple Makefile that compiles intbst.cpp and testbst.cpp.

A binary search tree class for integers, class IntBST is defined in intbst.h - please study this file for details of the class's features:

- In Step 1, the constructor, destructor, clear and insert methods are to be implemented in intbst.cpp. Notice the insert method will return false to indicate an attempt to insert a duplicate value; otherwise it inserts the value and returns true.
- In Step 2, you will implement the three print methods, pre-order, in-order, and post-order. 
- In Step 3 you will implement the sum, count, contains, and getNodeFor methods. 
- In Step 4, you will implement the predecessor, successor, and remove methods. Step 4 will likely take you the most time BY FAR, so plan accordingly.
The binary tree node structure is defined in the private area. The only instance variable is a node pointer, to point at the root node of the tree or at 0 if the tree is empty.
Several utility functions are declared in the private area too. These functions can be recursive (by virtue of their Node* parameters), and the public methods can use them. See how the destructor might use clear, for example, and how the insert method would use the overloaded version of insert, each by passing the root pointer to the corresponding utility function. Also take note of the definition of getNodeFor, which will be useful in several of the functions you need to implement. Consider implementing this function immediately after the print functions, and think about where you can reuse it.

# Step 1 - Constructor, Insert, Destructor, Clear

Use an editor (e.g., emacs) to make the following changes to intbst.cpp - do not change any of the other files.
First and foremost: fix the comment at the top to show your name(s) and the date.

Assuming you successfuly compiled in step 0a, you should be able to run testbst now:
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
  pre-order:
  in-order:
  post-order:
  sum: 0
  count: 0
  contains 64? N
  contains 4? N
  contains 16? N
  contains 128? N
  contains 17? N
  contains 512? N
  . . .
Empty BST:
  pre-order:
  in-order:
  post-order:
  sum: 0
  count: 0
  contains 16? N

```

As you can see, none of the functions do anything at the moment, but you can start by implementing the constructor and insert methods since these will server as the foundation for future testing. 
* Constructor: Even though the IntBST class may have many member functions associated with it, its only member variable is a Node* type called root. 
* Insert: Think about the properties of a binary search tree and traverse the tree accordingly. Note there is a private helper function for insert declared in intbst.h

Next, the destructor function, which uses a helper function called clear. 
* Clear: this method should remove all nodes in the binary search tree without creating memory leaks.
* Destructor: When the object's scope ends, the destructor should take care of any memory allocation during its lifetime.


# Step 2: Implement pre-order, in-order, and post-order binary tree printing

Now that we have the foundations for creating an object of IntBST, scroll to the print functions. Inside IntBST.h, you will notice there are both public and private implementations of the functions printPreOrder, printInOrder and printPostOrder. The private functions will be used as helpers to their public counterparts. Your job in this step is to implement all of them, public and private.
After you finish, save and then test your print implementations: compile and execute testbst again, choosing either all tests or just one of your print functions to test.
Here are the correct results (abbreviated to show just the print orders):

BST:

  pre-order: 64 8 4 32 16 128 512 256

  in-order: 4 8 16 32 64 128 256 512

  post-order: 4 16 32 8 256 512 128 64

By the way, you should be able to draw the tree now, both by tracing the order of the inserts, or by interpreting the three orders above. Take a minute to try that now on a piece of scratch paper since it may be very helpful when implementing the remaining functions.

# Step 3: Implement three more binary search tree functions

First: switch roles between pilot and navigator if you did not already do that.

You may do these tasks in any order. Check the results of each part as you complete it.

- Implement the helper function getNodeFor() - this function will be helpful for future functions.
- Implement the helper function for sum() - notice the public method just returns the result of the helper function. We suggest you use recursion to do so. Think about these questions before starting to code: What's the base case? What should be returned in the base case? What should be returned in the general (recursive) case?
- Implement the helper function for count() - this is very similar to the sum() function.
- Implement the public contains method, either recursively or iteratively - both are about the same level of difficulty in this case. If you decide to use recursion, you can use getNodeFor() in your implementation of contains(). You won't need this utility function to solve the problem iteratively. In either case, remember the tree is a binary search tree, and so your solution should run in O(log n) time.

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

# Step 7: Prepare a partner for the next lab
Please fill out this partner assignment form in preparation for lab05: <https://forms.gle/9JNewj6BnWaSeMnP6>

If you already have a partner, then please fill out this form now.
If you don't have a partner, and you want to be assigned one, then please fill out this form now. The TAs will assign you a partner based on some info about yourself.
If you don't have a partner, and you want to search for one, then please use the dedicated Piazza thread called Search for Teammates (this will help us avoid clutter on Piazza). After you find a partner, fill out this form.
If you wish to work alone, please still fill out this form to indicate your decision.
</div>
