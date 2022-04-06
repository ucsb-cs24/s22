---
layout: lab
num: lab01
ready: true
desc: "Linked Lists in C++ with structs"
assigned: 2022-04-06 23:59:00.00-8
due: 2022-04-12 23:59:00.00-8
---

# Pair programming is required for this lab
This is the only lab where pair programming is required.
The lab is identitical to lab09 from the Fall offering of CS16.
If you completed it as part of CS16, you may not simply resubmit that code.
Instead, we ask that you redo the lab with a partner, preferably someone who did not take CS16 in the Fall. The goal of the lab is to help students who don't have experience implementing a linked list get the practice they need.
By redoing the lab, you will be contributing to their learning and your own.

# Goals for this lab

The goal of this lab is to practice iterating through linked lists and solving problems through code tracing to reason about your code. 

We request that you DO NOT ask the staff to debug your code for you. They have been specifically instructed not to debug *for* you, but rather to *guide you* through the process of debugging your code yourselves.

# Step by Step Instructions

## Step 1: Getting Ready

Create a repo for this lab in our class organization and clone it to your local machine.


## Step 2: Obtain the starter code

The starter code is in this repo:

* <https://github.com/ucsb-cs24-s22/STARTER-lab01>

The URL for cloning this repo is this: `git@github.com:ucsb-cs24-s22/STARTER-lab01.git`


Once you've cloned the started code repo, typing the `ls` command on your machine should show you the following files in your current directory

```
$ ls
Makefile              linkedListFuncs.h	       tddFuncs.cpp
README.md             llTests.cpp		           tddFuncs.h
linkedList.h          moreLinkedListFuncs.cpp
linkedListFuncs.cpp	  moreLinkedListFuncs.h
```

## Step 3: Reviewing the files and what your tasks are

Here is a list of your tasks for this lab:

### Step 3a: Familiarize yourself with the big picture

Type "make tests" and you will see some tests pass, but some will fail.

You are finished when all the tests pass. We have implemented a few functions that involve linked lists in `linkedListFuncs.cpp`. There is only one file you need to edit this week:

<code>moreLinkedListFuncs.cpp</code> contains more functions that deal with linked lists.  


### Step 3b: Work on the linked list functions

Working on the linked list functions below is one of the most foundational things you can do to help you get ready for the rest of the curriculum.

There are 7 functions you will need to write for this lab:

* <code>addIntToEndOfList</code>
* <code>addIntToStartOfList</code>
* <code>pointerToMax</code>
* <code>pointerToMin</code>
* <code>largestValue</code>
* <code>smallestValue</code>
* <code>sum</code>


Each one has a set of tests which can be found under its corresponding heading when you type <code>make tests</code>. For example, the `addIntToEndOfList` tests look like this to start: 

```
./llTests 1
--------------ADD_INT_TO_END_OF_LIST--------------
PASSED: linkedListToString(list)
   FAILED: linkedListToString(list)
     Expected: [42]->[57]->[61]->[12]->null Actual: [42]->[57]->[61]->null
   FAILED: linkedListToString(list)
     Expected: [42]->[57]->[61]->[12]->[-17]->null Actual: [42]->[57]->[61]->null
PASSED: linkedListToString(empty)
   FAILED: linkedListToString(empty)
     Expected: [0]->null Actual: null
   FAILED: linkedListToString(empty)
     Expected: [0]->[19]->null Actual: null

```

You should replace each function stub with the correct code for the function until all of the tests for each one pass. It is recommended that you work on the functions one at a time in the order that they are presented above. That is, get all the tests to pass for `addIntToStartOfList`, then `addIntToEndOfList`, and so on. When all the tests pass, move on to the next step. 

## Step 4: Checking your work before submitting

When you are finished, you should be able to type  <code>make clean</code>, and then <code>make tests</code> to see the following output:


```
-bash-4.2$ make clean
/bin/rm -f llTests *.o
-bash-4.2$ make tests
g++ -Wall -Wno-uninitialized   -c -o llTests.o llTests.cpp
g++ -Wall -Wno-uninitialized   -c -o linkedListFuncs.o linkedListFuncs.cpp
g++ -Wall -Wno-uninitialized   -c -o moreLinkedListFuncs.o moreLinkedListFuncs.cpp
g++ -Wall -Wno-uninitialized   -c -o tddFuncs.o tddFuncs.cpp
g++ -Wall -Wno-uninitialized  llTests.o linkedListFuncs.o moreLinkedListFuncs.o tddFuncs.o -o llTests
./llTests 1
--------------ADD_INT_TO_END_OF_LIST--------------
PASSED: linkedListToString(list)
PASSED: linkedListToString(list)
PASSED: linkedListToString(list)
PASSED: linkedListToString(empty)
PASSED: linkedListToString(empty)
PASSED: linkedListToString(empty)
./llTests 2
--------------ADD_INT_TO_START_OF_LIST--------------
PASSED: linkedListToString(list)
PASSED: linkedListToString(list)
PASSED: linkedListToString(list)
PASSED: linkedListToString(empty)
PASSED: linkedListToString(empty)
PASSED: linkedListToString(empty)
./llTests 3
--------------POINTER_TO_MAX--------------
PASSED: pointerToMax(list1)
PASSED: pointerToMax(list1)
PASSED: pointerToMax(list1)->data
PASSED: pointerToMax(list1)->next->data
PASSED: pointerToMax(list2)
PASSED: pointerToMax(list2)
PASSED: pointerToMax(list2)->data
PASSED: pointerToMax(list3)
PASSED: pointerToMax(list3)
PASSED: pointerToMax(list3)->data
PASSED: pointerToMax(list4)
PASSED: pointerToMax(list4)
PASSED: pointerToMax(list4)->data
PASSED: pointerToMax(list4)->next->data
./llTests 4
--------------POINTER_TO_MIN--------------
PASSED: pointerToMin(list1)
PASSED: pointerToMin(list1)
PASSED: pointerToMin(list1)->data
PASSED: pointerToMin(list1)->next->data
PASSED: pointerToMin(list2)
PASSED: pointerToMin(list2)
PASSED: pointerToMin(list2)->data
PASSED: pointerToMin(list3)
PASSED: pointerToMin(list3)
PASSED: pointerToMin(list3)->data
PASSED: pointerToMin(list4)
PASSED: pointerToMin(list4)
PASSED: pointerToMin(list4)->data
PASSED: pointerToMin(list4)->next->data
./llTests 5
--------------LARGEST_VALUE--------------
PASSED: largestValue(list1)
PASSED: largestValue(list2)
PASSED: largestValue(list3)
PASSED: largestValue(list4)
./llTests 6
--------------SMALLEST_VALUE--------------
PASSED: smallestValue(list1)
PASSED: smallestValue(list2)
PASSED: smallestValue(list3)
PASSED: smallestValue(list4)
./llTests 7
--------------SUM--------------
PASSED: sum(list1)
PASSED: sum(list2)
PASSED: sum(list3)
PASSED: sum(list4)

-bash-4.2$
```

At that point, you are ready to try submitting on Gradescope.


## Step 5: Turn in your code on Gradescope

Submit all the `.cpp` and `.h` files to the lab01 assignment on Gradescope via your github repo. Then visit Gradescope and check that you have a correct score.

* You must check that you have followed these style guidelines:

1. Indentation is neat, consistent, and follows good practice. e.g. code that is inside braces should be indented, and code that is at the same "level" of nesting inside braces should be indented in a consistent way.
2. Variable name choice: variables should have sensible names.

Follow examples from lectures, sample codes, and from the textbook.   
Always commit and push the latest version of your code to github

## An important word about academic honesty and the gradescope system

We will test your code against other data files too&mdash;not just these.  So while you might be able to pass the tests on gradescope now by just doing a hard-coded "cout" of the expected output, your submission will NOT receive credit.    

To be very clear, code like this will pass on gradescope, BUT IT REPRESENTS A FORM OF ACADEMIC DISHONESTY since it is an attempt to just "game the system", i.e. to get the tests to pass without really solving the problem.

I hope this is obvious, but I have to state it so that there is no ambiguity: hard coding your output is a form of cheating, i.e. a form of "academic dishonesty".  Submitting a program of this kind would be subject not only to a reduced grade, but also to possible disciplinary penalties. If there is <em>any</em> doubt about this fact, please ask your TA and/or your instructor for clarification.

## Logging out

If you are logged in remotely on CSIL, you can log out using the exit command:

```
$ exit
```


