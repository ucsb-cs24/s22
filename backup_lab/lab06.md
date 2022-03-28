---
layout: lab
num: lab06
ready: true
desc: "Implementing a heap"
assigned: 2021-05-27 13:00:00.00-8
due: 2021-06-02 21:59:00.00-7
---

# Goals for this lab

By the time you have completed this lab, you should be able to

* Understand the purpose and behavior of a priority queue
* Understand how to implement an array-based heap

This lab may be done with a partner

## Step by Step Instructions

# Step 0: Surveys (1% of your overall grade)

Please complete the following two surveys to receive 1% extra credit on your overall grade. Each survey is worth 0.5%


## Survey: Complete the TA/Mentor evaluations

 This is an anonymous survey but its setup in a way that at the end you can still get credit for filling it. At the end of the survey you are directed to a separate survey where you should enter your credentials to get credit.

Survey to get your feedback about the CS24 curriculum:
[https://ucsb.co1.qualtrics.com/jfe/form/SV_0PKZjij05RB0XgF](https://ucsb.co1.qualtrics.com/jfe/form/SV_0PKZjij05RB0XgF)

The survey counts towards 4% of the grade for this lab

## Step 1: Get the starter code
Use scp to copy the starter code from CSIL from the following directory:

[Lab06-data](https://github.com/ucsb-cs24-mirza-s21/lab06_starter_code)


You should have the following files:

```
-bash-4.3$ ls
examheap.cpp heap.cpp heap.h
```

First look at heap.h to see the basic operations for a heap. You will implement all of these operations for these lab. Also notice the storage mechanism we will be using for the heap: a [http://www.cplusplus.com/reference/vector/](http://www.cplusplus.com/reference/vector/). It will probably be a good idea to read through the documentation for this standard library class (linked above) if you are not familiar with it.

Now look at examheap.cpp. This file will test your heap's behavior. The first test is quite simple and just adds a couple elements to your heap. For larger numbers of inputs, it uses the `std::priority_queue` class from the standard library as ground truth to test your code against. The first thing you need to do is compose your Makefile to compile `examheap.cpp` with `heap.cpp` to executable `examheap`. Then, feel free to compile and run `examheap` before starting on your code. However, note that all the tests will fail and say "Aborted (core dumped)".

## Step 2: Implement the functions of heap.cpp

There are four functions you need to implement in heap.cpp: `push`, `pop`, `top`, and `empty`. Note that only `push` and `pop` modify the heap, while `empty` and `top` only return values. When testing your code, be sure to run the large tests (4 and 5) to find any minor bugs in your code that may not show up on the smaller tests.

You are allowed to add helper functions in heap.h and heap.cpp if you need them. However, you should use the vector in heap.h as the underlying storage for your heap.

## Step 3: Submit heap.cpp and heap.h

Submit the files heap.cpp, heap.h, and Makefile to the lab06 assignment on Gradescope.

## Evaluation and Grading

Each student must accomplish the following to earn full credit for this lab:
[70 points] heap.cpp and heap.h are saved, with your name(s) in a comment at the top and other evidence of your work. Both of these files should compile and execute properly too.


