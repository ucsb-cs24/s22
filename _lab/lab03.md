---
layout: lab
num: lab03
ready: false
desc: "Implementing a linked list- OOP style"
assigned: 2022-04-20 9:00:00.00-8
due: 2022-04-27 23:59:00.00-8
---

## Announcing your collaboration choice 
This lab may be done with a partner or solo. 
You can choose to work with the same partner as lab02, form a new partnership, or ask the TAs to assign you a partner.
However, you must fill out this form to announce your decision:
<https://forms.gle/wa5whZc72mmugmW8A>


If you have identified a partner in your section who has also agreed to work with you or if you decide to work solo, you can begin working on the lab right after submitting the form.

However, if you are requesting for the TAs to assign a partner to you, you must wait until your section time on Thursday to hear about the assignment.  Please respond to any communication from TAs or your partners quickly! Not responding to your partner by more than a day will lead to a 30% deduction in your grade.

If you missed the deadline, you must still fill the form before you begin working on this lab to get credit for the lab.

# Goals for this lab

By the time you have completed this lab, you should be able to

* Explain the meaning of a "self-referential" data structure
* Create, use and manage memory for simple linked lists
* Implement functions that process linked lists




# Academic Honesty 
All work submitted for this lab should be your own and your partners. If you are using any hints from a previous offering of this course that was posted publicly by a CS24 instructor, you must cite your source. 

# Step by Step Instructions

## Step 1: Create a directory and get files


* Create a repo for this lab in our class organization following the correct naming convention
* Clone your repo in your cs24 directory on CSIL.  
* Navigate to your starter-code directory and do a git pull to get the latest version of the code.
* Change into your {{page.num}} git directory
* Now copy all of the files for this lab from the starter-code directory to your git directory:

Visit the following web link—you may want to use “right-click” (or “control-click” on Mac) to bring up a window where you can open this in a new window or tab:

[{{page.num}} Files](https://github.com/{{site.class_org.name}}/{{page.num}}_starter/)


You should see a listing of several C++ files. Please copy those files into your local lab03 Github repo directory.

Typing the list (ls) command should show you the following files in your current directory:


```
-bash-4.2$ ls
intlist.cpp  intlist.h  Makefile  README.md  testlist.cpp  testrest.cpp
-bash-4.2$  make all
g++ -c -g testlist.cpp
g++ -c -g intlist.cpp
g++ -g -o testlist testlist.o intlist.o
g++ -c -g testrest.cpp
g++ -g -o testrest testrest.o intlist.o
```

We will discuss these files in Step 3. But first some practice.

## Step 2: Practice using linked structures (Optional)

You can go to the website, "www.cpp.sh", to practice the linked structures. (Or any other online cpp shell)
Type or copy/paste the simple program shown below (in bold) at the code area in cpp.sh (replacing the original sample code):

The structure, 'Node', you just created incorporates a way for an object of its type to point at another object of the same type - it is a self-referential structure. The idea is to point the next field of a Node at another Node, and in this way we can build lists of Nodes, with each one pointing to the next one. We also maintain a separate pointer that points at the first node in the list - often we call this pointer the "list" because it is the way we can access the list's elements.

But before we do all that, let's just make a Node object, set it's fields, and let us display its contents:

```
#include <iostream>

struct Node {int info; Node *next;};

int main()
{
  Node item;
  item.info = 9;
  item.next = 0;
  std::cout << "This node holds a number: " << item.info << "\n";
}
```

Now click a "Run" button below the code area.
You shall see the output in the bottom.

```
This node holds a number: 9
```

The Node named item stores a 9 as its information, and its next field (a.k.a. "link") does not point to anything. (The address 0 is reserved to mean "no address" in C++, and it is also the value of the symbolic constant NULL that is defined in cstdlib. Notice that ch calls it nil, but that just means the same thing too.) Usually a node with a null link is used to indicate the end of a linked list.

Now let's use the structure to build an actual linked list of three integers. First we will declare a pointer named list to point at the first node in the list (or null if the list is empty). We initialize this pointer to a dynamically allocated first node, using the C++ keyword new (which returns a pointer). The remaining steps will create two more nodes, store values in each node, and properly link them all together as a list. Type or copy/paste the program in bold:

```
#include <iostream>

struct Node {int info; Node *next;};

int main()
{
  Node* list = new Node;
  list->info = 10;
  list->next = new Node;
  list->next->info = 20;
  list->next->next = 0;
  
  Node* temp = list;
  list = new Node;
  list->info = 5;
  list->next = temp;
  
  for (Node* n = list; n != 0; n = n->next) {
    std::cout << "\nThis node is at address: " << n << std::endl;
    std::cout << "It holds a number: " << n->info << std::endl;
    std::cout << "Moving to the next node whose address is " << n->next << "..." << std::endl;
  }
}
```

Now click a "Run" button below the code area.
You shall see the output in the bottom.

```
This node is at address: 0x16359e0
It holds a number: 5
Moving to the next node whose address is 0x16359a0...

This node is at address: 0x16359a0
It holds a number: 10
Moving to the next node whose address is 0x16359c0...

This node is at address: 0x16359c0
It holds a number: 20
Moving to the next node whose address is 0...
```

The for loop continues as long as n points at a node. At the end of each loop iteration, n is changed to point at the next node in the list. Study this loop, and be sure to understand it - discuss it with your partner to make sure you both understand it.

As one more illustration, let's use a while loop to count the nodes in a list like this one. Make sure you understand the following loop too, in which the while loop condition is just the node pointer itself -- it becomes 0 at the end. ;-)

```
#include <iostream>

struct Node {int info; Node *next;};

int main()
{
  Node* list = new Node;
  list->info = 10;
  list->next = new Node;
  list->next->info = 20;
  list->next->next = 0;
  
  Node* temp = list;
  list = new Node;
  list->info = 5;
  list->next = temp;
  
  Node* n = list;
  while (n) {
    std::cout << "\nThis node is at address: " << n << std::endl;
    std::cout << "It holds a number: " << n->info << std::endl;
    std::cout << "Moving to the next node whose address is " << n->next << "..." << std::endl;
    
    n = n->next;
  }
}
```

One big issue in the above program is memory leak.

Since we dynamically allocated the memory for three nodes, we should free that memory before exiting the program and proceeding to Step 3. Also, according to convention, we set the list pointer to null - it is now an empty list:

```
#include <iostream>

struct Node {int info; Node *next;};

int main()
{
  Node* list = new Node;
  list->info = 10;
  list->next = new Node;
  list->next->info = 20;
  list->next->next = 0;
  
  delete list->next; // Why we free list->next firstly?
  delete list;
  list = 0; // Can we put this line before delete line?
}
```

## Step 3: Learn how to encapsulate list nodes

Now that you have a feel for list nodes, you should know that such structures are not usually manipulated directly by application programs - not in C++ anyway (although it is common in C programming). Instead applications normally use objects of a List class, and the class itself is the only part of the program that accesses list nodes.

In the rest of this lab, you will help build such a list class. The class definition is stored in intlist.h - please study it to know its parts:

The public declarations show what a client program can do with an IntList object. Notice, however, that the list node structure definition is in the private area. Clients can't directly use or even refer to such nodes, but all that clients should care about are the values stored in these nodes anyway! Also notice that every list object will have one node pointer, to point at the first node in the list or at 0 if the list is empty.
Now look at intlist.cpp. The functions that you need to implement are marked in that file. Some of the methods of the class are implemented at the bottom of the file - do not change what is done.

An application file would create IntList objects and use them to solve problems. For this lab, we have two application files, both of which are testing programs - testlist.cpp and testrest.cpp. First look testlist.cpp. Two IntList objects are created; then numbers read from the command line are appended to one of the lists; and finally the methods are tested for each list.

You can use the provided Makefile to help you complile the program. 

## Step 4: Implement linked list functions


You should be able to run the program now (assuming you compiled it in Step 3) - it requires you to enter a starter list of integers on the command line:

```
-bash-4.2$ ./testlist
error: need at least one int arg on command line
usage: ./testlist int [int ...]
```

Next time we'll run it properly. The contains method is checked for three values that ought to be in the list, plus one value that should not (the sum). Here is a sample run with initial values of 5, 7, 9 and 11:

```
./testlist 5 7 9 11
List 1:
   [5 7 9 11]
   count: 4
   sum: 0
   contains 5 ? no
   contains 7 ? no
   contains 11 ? no
   contains 0 ? no
   max: 0
   average: 0.000
   List after insertFirst(sum):
   [5 7 9 11]
Empty list 2:
   []
   count: 0
   sum: 0
   contains 1 ? no
   max: 0
   average: 0.000
   List 2 after insertFirst(3), then insertFirst(1):
   []
```
See that append, print and count all work. But the others need to be fixed. 

Use an editor (e.g., emacs or vim) to make the following changes to intlist.cpp - do not change any of the other files.

* Fix the comment at the top to show your name and the date.
* Implement the sum method. See the count method for guidance.
* Save, and then test your sum implementation - compile and execute testlist again. Verify sum is working before going on.
* Push your code to github using the "git add .", "git commit" and "git push " commands
* Then implement the contains method, save again and test again.
* Continue with the other three functions in the same way: implement and test one at time. Don't implement the copy constructor, destructor and assignment operator yet.

Push your code to github often. 

Here are correct results for the same sample data as above:

```
List 1:
   [5 7 9 11]
   count: 4
   sum: 32
   contains 5 ? yes
   contains 7 ? yes
   contains 11 ? yes
   contains 32 ? no
   max: 11
   average: 8.000
   List after insertFirst(sum):
   [32 5 7 9 11]
Empty list 2:
   []
   count: 0
   sum: 0
   contains 1 ? no
   max: 0
   average: 0.000
   List 2 after insertFirst(3), then insertFirst(1):
   [1 3]
```

Ask yourself: With just the automatic copy constructor and assignment operator, won't copies be shallow? 

You will fix this problem by overloading the copy constructor and assignment operator. You should also implement the destructor. However before you begin, examine testrest.cpp. This file tests the functions your are about to implement.

Run the test program with argument 1 (to test your copy constructor) before implementing the above functions.

```
$ ./testrest 1
Segmentation fault (core dumped)
```
Now run the program with the same argument in gdb and try to figure out exactly why it crashed.

* Implement the copy constructor in intlist.cpp. Compile with make and run <code>$ ./testrest 1</code>. Repeat this process until the test passes. However its not enough to just pass the test. This because when you are writing programs that work with dyanamic data (on the heap), your program could have memory leaks that are not captured by unit tests. To check for leaks you should run your program in valgrind as follows:

```
$ valgrind --leak-check=full ./testrest 1
==5414== Memcheck, a memory error detector
==5414== Copyright (C) 2002-2015, and GNU GPL'd, by Julian Seward et al.
==5414== Using Valgrind-3.12.0 and LibVEX; rerun with -h for copyright info
==5414== Command: ./testrest 1
==5414== 
PASSED copy constructor tests
==5414== 
==5414== HEAP SUMMARY:
==5414==     in use at exit: 0 bytes in 0 blocks
==5414==   total heap usage: 17 allocs, 17 frees, 73,968 bytes allocated
==5414== 
==5414== All heap blocks were freed -- no leaks are possible
==5414== 
==5414== For counts of detected and suppressed errors, rerun with: -v
==5414== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
```

The error summary should show 0 errors as shown above. If you have memory leaks, valgrind will let you know.


* Implement the destructor, compile and run <code>$ ./testrest 2</code>. 
You should see the following message:

```
$ ./testrest 2
Testing destructor, run in valgrind to check for leaks
```
Now run it in valgrind to make sure you don't have any memory leaks

* Finally implement the overloaded assignment operator in intlist.cpp. To test it run <code>$ ./testrest 3</code>. If it doesn't crash, run it in valgrind to check for memory leaks

## Step 5: Submit intlist.cpp and intlist.h (if you have modified it).

Log into your account on https://www.gradescope.com/ and navigate to our course site. Select this assignment. Then click on the "Submit" button on the bottom right corner to make a submission. You will be given the option of uploading files from your local machine or submitting the code that is in a github repo. Select the second option and select your github repo for this assignment. You should receive 100/100 for a completely correct program.


Do beware that all parts must be working to earn any points at all from the Gradescope system.


## Evaluation and Grading

Each student must accomplish the following to earn full credit for this lab:

* [100 points] intlist.cpp is saved, it has your name(s) in a comment at the top, it compiles and executes properly, and has been submitted with a score of 100/100 to the Gradescope system.




