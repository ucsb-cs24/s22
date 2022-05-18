---
layout: lab
num: lab05
ready: true
desc: "Generic Binary Search Tree"
assigned: 2022-05-11 15:00:00.00-8
due: 2022-05-20 23:59:00.00-8
---
<div markdown="1">

# Collaboration policy

May be done solo or with a partner. 

Note that this assignment was previously an extra credit portion of lab04. However, since generic programming is one of the topics that you will be assessed on, completing this lab is required and not just extra credit. 

# Goals
Your task is to convert your BST from lab04 to work with any generic type of keys (i.e. not just `int` types). 
For convenience, we will not change any of the file or data structure names, but your BST should be useable as `IntBST<T>` 
where `T` is a type that can be compared with `<`, `>`, `==` etc. 
`T` can be a `double`, `char`, or any other type for which relational operators have been defined.  

You must modify all of the code in the files `intbst.cpp  intbst.h` to be consistent with handling keys of generic type `T`. 
To do this you will need to use the concept of templates in C++.

Since templates only provide a blueprint for the defintion of a class (or function), your implementations of the class `IntBST<T>` in `intbst.cpp` and `intbst.h` cannot be compiled to machine code directly. 
This is because the compiler doesn't know how to instantiate the template parameter, `T`, of the class. 

Instead, the compiler needs additional context on how the class is used and the type of data it works with to generate the code. 
This additional context is provided when objects of type `IntBST<T>` are declared, and the template parameter is specified to be a particular value/type. 

For this reason, you shouldn't try to compile `intbst.cpp` as a separate object file, 
but instead, `#include intbst.cpp` right after the class definition in `intbst.h`.

Your `intbst.h` should be structured as follows:

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

Submit both `intbst.cpp` and `intbst.h` to the lab05 assignment on Gradescope. 

# Prepare a partner for the next lab
Please fill out this partner assignment form in preparation for lab06: <https://forms.gle/vaUuLV7FRr3f328N6>

* If you already have a partner, then please fill out this form now.
* If you don't have a partner, and you want to be assigned one, then please fill out this form now. The TAs will assign you a partner based on some info about yourself.
* If you don't have a partner, and you want to search for one, then please use the dedicated Piazza thread called Search for Teammates (this will help us avoid clutter on Piazza). After you find a partner, fill out this form.
* If you wish to work alone, please still fill out this form to indicate your decision.

</div>
