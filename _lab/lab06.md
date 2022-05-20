---
layout: lab
num: lab06
ready: true
desc: "Evaluating expressions with stacks"
assigned: 2022-05-19 20:00:00.00-8
due: 2022-05-26 23:59:00.00-8
---

# Collaboration policy
This lab may be done solo or with a partner of your choice.

# Goals for this lab

By the time you have completed this lab, you should be able to

* Understand the meaning and purpose of typical stack operations
* Solve problems with the help of stacks, including stack<T> objects from the Standard Template Library
* Evaluate expressions in postfix form


## Step by Step Instructions

## Step 1: Create a {{page.num}} git repo and get the starter code

First get together with your lab partner. If your regular partner is more than 5 minutes late, let your mentor know.

Select a pilot, log into the CSIL machines.

## Step 1: Get the starter code

Get the starter code from this repo:
<https://github.com/ucsb-cs24-s22/STARTER-lab06>

Check that you have the following files

```
-bash-4.3$ ls
evalfull.cpp  intstack.h  usestack.cpp
```

First look at `intstack.h to learn what you can do with objects of this type. You can also notice how a stack can be implemented with an array - since all of the methods are very simple, they are implemented "inline" as part of the function definition.

Now look at usestack.cpp - notice it starts with `#include "intstack.h"` so it can create objects of type Stack and use the public methods of that class. The main function creates a Stack object named s, then it pushes first 10 then 20 onto the stack.

Finally, it loops until the stack is empty, printing the top element then popping that element from the stack. Feel free to compile it and run it - notice the numbers are popped from the stack in last-in first-out (LIFO) order:

```
-bash-4.3$ make usestack
g++     usestack.cpp   -o usestack
-bash-4.3$ ./usestack
20
10
```
Edit `usestack.cpp` with emacs or another editor to play with this stack until you are comfortable with its operations.

Push some numbers, pop a few numbers, use cout to print the top number, and so on.
You might want to leave the loop at the end alone, to print out the remaining numbers at the end. Try to predict what numbers will be printed, and in what order.

Move on to **Step 3** after you are sure you know how to use this ADT.

WARNING: this stack does no error checking - do not push a number onto it if it already has 10 of them, and do not try to access the top element if the stack is empty!

## Step 3: Learn an algorithm that uses stacks, and implement it

The next file to look at is evalfull.cpp which is intended to evaluate fully-parenthesized arithmetic expressions. You can compile and run it now, but no matter what expression the user enters, it will say "bad expression: parentheses are not balanced" until you implement the function named balanced. But first learn how two stacks can be used to evaluate an arithmetic expression that has a set of parentheses enclosing every calculation. For example, the first expression below is fully parenthesized, and the rest are not:

( 4 * ( ( 5 + 3.2 ) / 1.5 ) )  // okay

( 4 * ( ( 5 + 3.2 ) / 1.5 )    // unbalanced parens - missing last ')'

( 4 * ( 5 + 3.2 ) / 1.5 ) )    // unbalanced parens - missing one '('

4 * ( ( 5 + 3.2 ) / 1.5 )      // not fully-parenthesized at '*' operation

( 4 * ( 5 + 3.2 ) / 1.5 )      // not fully-parenthesized at '/' operation

The main function gets an expression from the user, assuming that the "tokens" are separated by spaces. Each part of the expression is a different token - left parenthesis, right parenthesis, number, and arithmetic operators add, subtract, multiply and divide. These tokens are stored in an array, char *expression[] and passed to the evalFull function inside a try block, where it prints the result returned by `evalFull`. The `evalFull` function might throw a string exception if the expression cannot be evaluated, and such exceptions are caught and printed by main.

Understand the `evalFull` algorithm provided to you (as well as the utility function that identifies tokens and the enum TokenType). Try to follow the steps involved, and see how the program implements them.

You must write function `balanced` to complete this program by editing evalFull.cpp. The algorithm was discussed in lecture. Just one stack is needed, and it is already created in the skeleton: stack<char *> s is an object of the STL stack class that is set up to store C strings like "(".
Compile and test it on some balanced and some unbalanced expressions. If balanced, the program should print a result, or at least throw a different exception string like the following sample runs of our solution:

```
-bash-4.3$ ./evalfull
enter expression: ( 4 + 7 )
result: 11
-bash-4.3$ ./evalfull
enter expression: ( 4 + 7 / 2 )
bad expression: operator(s) left on stack at end
-bash-4.3$ ./evalfull
enter expression: ( 4 7 )
bad expression: empty stack where operator expected

```

## Step 4: Submit evalfull.cpp and usestack.cpp

Submit the files `evalfull.cpp` and `usestack.cpp` to the assignment on Gradescope.

## Evaluation and Grading

Each student must accomplish the following to earn full credit for this lab: usestack.cpp and evalfull.cpp are saved, with your name(s) in a comment at the top and other evidence of your work. Both of these files should compile and execute properly on Gradescope.



## Optional Extra Challenge

Improve class Stack (the one defined in intstack.h) so its functions will behave properly if called on an empty or full stack.

Notice what pop does now, for example: it decrements next no matter how many times it is called on an empty stack, which essentially is a seg fault waiting to happen when top is called or even push in some cases. At least pop should check for an empty stack and decrement only when it is not. Also both top and push should throw exceptions when they are used improperly, and the class should provide a way to check for a full stack.

First, create intstack.cpp for implementing the functions of class Stack. The reason is that your functions won't be "one-liners" anymore, and therefore they are inappropriate choices for inline functions. Cut all of the implementations from intstack.h (constructor and four member functions) and paste them into intstack.cpp, and make all other necessary syntax changes. When done, verify it still compiles and that it works correctly with usestack.cpp too.

Add a function, bool full() const, that returns true if the stack is filled to its capacity. Add the declaration in intstack.h, implement it in intstack.cpp, and add a test for it in usestack.cpp.

Also in intstack.cpp:
Implement push to throw string("full stack") if it is called when the stack is full.

Implement pop to not decrement next if the stack is empty.

Implement top to throw string("empty stack") if it is called when the stack is empty.

Test all of these changes by editing usestack.cpp again (requires a try/catch block at least).

Improve class Stack even more by preventing it from ever getting full. This challenge requires that you redesign the private portion of the class. Choose one of the following options:

Use a dynamically allocated array that grows as necessary.

The instance variable, data, must be changed (in intstack.h) from an int array to an int pointer. You should also add an instance variable to store the current capacity, and you can delete the CAPACITY symbolic constant.

Change the constructor implementation (in intstack.cpp) to dynamically allocate an array of ints, as in data = new int[10], and set the value of the current capacity (to 10 in this case).

Change the implementation of push so instead of throwing an exception if the array is currently at capacity, it dynamically allocates more space and always pushes the int passed to it. Update the capacity variable too. Choices here are to double the current capacity, or maybe just add 10 more, but either way it will be necessary to copy the values from the old array, delete[] the old array, and set data to point at the new array.

Change the implementation of full to return false every time it is called.

Use a linked list.

For this option the private portion of the class (in intstack.h) must define a node structure, and an instance variable that points to the first node - traditionally treated as the "top" of the stack. There really is no need for any other instance variables.

The implementations of push, pop, top and empty all must be changed accordingly, and full always should return false.
In either case, test your stack implementation with a variation of usestack.cpp.
