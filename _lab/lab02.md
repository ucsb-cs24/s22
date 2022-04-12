---
layout: lab
num: lab02
ready: true
desc: "Objective Cars"
assigned: 2022-04-13 15:00:00.00-8
due: 2022-04-19 23:59:00.00-8
---

# Pair programming for this lab

This lab may be done solo or in pairs. Before you begin working on the lab, please decide whether you will work solo or with a partner. If you decide to work with a partner, there are a few requirements you must follow:
* You and your partner must agree to work together outside of the lab section in case you do not finish the lab during your lab section. You are responsible for exchanging contact information in case you need to reach your partner.
* If you choose to work with a partner for a future lab where pair programming is allowed, then you must choose a partner you have not worked with before.
* You MUST add your partner on Gradescope when submitting your work EACH TIME you submit your file(s). After uploading your file(s) on Gradescope, there is a “Group Members” link at the bottom (or “Add Group Member” under “Groups”) where you can select the partner you are working with. Whoever uploaded the submission must make sure your partner is part of your Group. Click on “Group Members” -> “Add Member” and select your partner from the list.
* You must write your Name(s) and Perm number on each file submitted to Gradescope.
Once you and your partner are in agreement, choose an initial driver and navigator, and have the driver log into their account.

# Step by Step Instructions

## Step 1: Getting Ready

Create a repo for this lab in our class organization and clone it to your local machine.

## Step 2: Get the starter code

The starter code is in this repo:

* <https://github.com/{{site.class_org.name}}/STARTER-lab02>

Please get the starter code in the same way as lab01. This is a great opportunity to practice working with git and GitHub!

Once you've gotten the starter code, typing the `ls` command on your machine should show you the following files in your current directory:
```
$ ls
car.cpp  car.hpp  doors.hpp  perf.cpp  perf.hpp
```

If you don't see those files, go back through the initial instructions from lab01 and make sure you didn’t miss a step. If you still have trouble, ask your TA/ULAs for assistance.

## Step 2: Understand the Code and Finish car.cpp 

In this lab you will create a comprehensive `Car` class with
* descriptive member variables, 
* constructor, 
* copy constructor, 
* destructor, 
* overloaded assignment operators, and
* commonly used methods that manipulate member variables

The definition of the `Car` class will be provided to you in the header file `car.hpp`. The member variables listed below are all private:
```
char*  manufacturer;
char*  model;
uint32_t  zeroToSixtyNs;
float  headonDragCoeff;
uint16_t  horsepower;
DoorKind  backseatDoors;
uint8_t  seatCount;
```

The functionalities of these variables can easily be inferred from their names. The `manufacturer` and `model` are of the type `string`, e.g. `manufacturer = "Audi\0"` and `model = "R8\0"`, which shall be dynamically managed. `zeroToSixtyNs` is the time taken to accelerate from 0 to 60 mph. There are also `headonDragCoeff`, `horsepower`, and `seatCount`. The `backseatDoors` is an enumeration whose declaration is in `doors.hpp`. It can take one of the four values: 
1. `None = 0`, 
2. `Hinge = 1`, 
3. `GullWing = 2`, 
4. `Sliding = 3`

The descriptions of the functionalities of the public methods are listed below:

* `Car()`
	* Default constructor. Initialize the pointer type variables with `NULL` and the numerical variables with `0`. `DoorKind` variable is also initialized with `None`.
* `Car(char const* const manufacturerName, char const* const modelName, PerformanceStats perf, uint8_t numSeats, DoorKind backseatDoorDesign)`
	* Constructor. Initialize the member variables with specific values.
* `Car(Car const& o)`
	* Copy constructor. Initialize the member variables with the values in `o`.
* `~Car()`
	* Destructor. Recycle the memory of variables.
* `Car& operator=(Car const& o)`
	* Overloaded assignment operator `=`. Set the values of the variables in the current object to be those in `o`.
* `char const* getManufacturer() const`
	* Get the string of `manufacturer`.
* `char const* getModel() const`
	* Get the string of `model`.
* `PerformanceStats getStats() const`
	* `PerformanceStats` is a structure given to you in the head file `perf.hpp`. It summarizes the three parameters `horsepower`, `zeroToSixtyNs`, and `headonDragCoeff` together. This method gets their values and returns as the structure.
* `uint8_t getSeatCount() const`
	* Get the number of seats in `seatCount`.
* `DoorKind getBackseatDoors() const`
	* Get the type of the doors in `backseatDoors`.
* `void manufacturerChange(char const* const newManufacturer)`
	* Change the name (string) in `manufacturer` to the new in `newManufacturer`. Since the name is of the type string in the memory, please care about the memory management and avoid the memory leak.
* `void modelNameChange(char const* const newModelName)`
	* Change the name (also string) in `model` to the new in `newModelName`.
* `void reevaluateStats(PerformanceStats newStats)`
	* Update the values of `zeroToSixtyNs`, `headonDragCoeff` and `horsepower` by using the new parameters in `newStats`.
* `void recountSeats(uint8_t newSeatCount)`
	* Set the value of `seatCount` to be `newSeatCount`.
* `void reexamineDoors(DoorKind newDoorKind)`
	* Set the kind of the doors in `backseatDoors` to be `newDoorKind`.


## Step 3: Test Your Code and Upload to Gradescope

The Autograder will use some test cases to check if your implementations are correct. In order to verify them, you’ll need to write your own test code, which can be a ‘main’ function to print out the results, before the submission. Then, write a Makefile to link all dependencies to make and run your test. 
The lab assignment “Lab02” should appear in your Gradescope dashboard in CS 24. If you haven’t submitted anything for this assignment yet, Gradescope will prompt you to upload your files. For this lab, you will only need to upload your modified file (i.e. `car.cpp`). 
If you already submitted something on Gradescope, it will take you to their “Autograder Results” page. There is a “Resubmit” button on the bottom right that will allow you to update the files for your submission.
For this lab, if everything is correct, you’ll see a successful submission passing all of the Autograder tests.

**Remember to add your partner to Group Members for this submission on Gradescope if applicable. At this point, if you worked in a pair, it is a good idea for both partners to log into Gradescope and check if you can see the uploaded files for Lab02.**
