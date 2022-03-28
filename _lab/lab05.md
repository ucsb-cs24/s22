---
layout: lab
num: lab05
ready: true
desc: "Generic Binary Search Tree"
assigned: 2022-02-17 9:00:00.00-8
due: 2022-02-23 22:00:00.00-8
---
<div markdown="1">

# Collaboration policy

May be done solo or with the same partner as lab04. 

Before completing this lab see the video recording of Lecture 13 on templates on Gauchospace.

Note that this assignment was previously an extra credit portion of lab04. However, since generic programming is one of the topics that you will be assessed on, completing this lab is required and not just extra credit. If you already completed the previously "extra credit" portion of lab04 and received a full score, then you have effectively completed this assignment

# Goals
Your task is to convert your BST from lab04 to work with any generic type of keys (not just ints). For convenience, we will not change any of the file or data structure names, but your structure should be useable as IntBST<T> where T is a type that can be compared with <, >, == etc. This could include double, char, or any other type for which relational operators have been defined.  You must modify all of the code in the files `intbst.cpp  intbst.h` to be consistent with handling keys of generic type T. To do this you will need to use the concept of templates in C++.

Since templates only provide a blueprint for the defintion of a class (or function), your implementations of the class IntBST<T> in intbst.cpp and intbst.h cannot be compiled to machine code directly. That's because based on that code, the compiler doesn't know how to instantiate the template parameter of the class. Instead the compiler needs additional context on how the class was used to generate the code. This happens when objects of type IntBST<T> are declared and the template parameter if specified to be a particular value. For this reason you shouldn't try to compiler intbst.cpp as a separate object file. Instead, include intbst.cpp right after the class definition in intbst.h.

So, your intbst.h should be structured as follows:

```
#ifndef INTBST_H
#define INTBST_H

#include <iostream>

using namespace std;

// Replace the following existing definition of IntBST with the new class definition

class IntBST {
    ...
    ...

};
//end of class definition

#include "intbst.cpp" 

#endif
```

Submit both intbst.cpp and intbst.h to the lab05 assignment on Gauchospace. 


</div>
