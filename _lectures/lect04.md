---
num: "lect04"
desc: "Operator Overloading, Organizing C++ programs using multiple files and Makefiles "
ready: ready
pdfurl: /lectures/CS24_Lecture4.pdf
annotatedpdfurl: /lectures/CS24_Lecture4_ann.pdf
annotatedready: false 
lecture_date: 2022-01-13
---

# Code from lecture
[{{site.lect_repo}}/tree/main/{{page.num}}]({{site.lect_repo}}/tree/main/{{page.num}})

# Lesson plan
- Starting with the code from the previous lecture where everything was implemented in a single cpp file, we will split the program into a header file (that only contains declarations) and cpp files (containing the implemenation of the complex class's member functions and test code). A more modular organization of code is desirable for readability, debugging, and maintenance.
- How to compile a program that is split across multiple files by writing an appropriate Makefile
- Correct use of #include 
- Operator overloading (updated implementation of the stream operator << for the complex class)
