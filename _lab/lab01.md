---
layout: lab
num: lab01
ready: true
desc: "Objective Cars"
assigned: 2022-01-13 9:00:00.00-8
due: 2022-01-19 22:00:00.00-8
---

# Goals Step by Step

## Step 0: Getting Started

This lab may be done solo, or in pairs.
Before you begin working on the lab, please decide if you will work solo or with a partner.
As stated in previous labs, there are a few requirements you must follow if you decide to work with a partner. I will re-iterate them here:
* Your partner must be enrolled in the same lab section as you.
* You and your partner must agree to work together outside of the lab section in case you do not finish the lab during your lab section. You must agree to reserve at least two hours outside of the lab section to work together if needed. You are responsible for exchanging contact information in case you need to reach your partner.
* If you choose to work with a partner for a future lab where pair programming is allowed, then you must choose a partner you have not worked with before.
* You MUST add your partner on Gradescope when submitting your work EACH TIME you submit your file(s). After uploading your file(s) on Gradescope, there is a “Group Members” link at the bottom (or “Add Group Member” under “Groups”) where you can select the partner you are working with. Whoever uploaded the submission must make sure your partner is part of your Group. Click on “Group Members” -> “Add Member” and select your partner from the list.
* You must write your Name(s) and Perm number on each file submitted to Gradescope.
Once you and your partner are in agreement, choose an initial driver and navigator, and have the driver log into their account.

## Step 1: Copying some programs from my directory
Visit the following web link—you may want to use “right-click” (or “control-click” on Mac) to bring up a window where you can open this in a new window or tab:

[Lab01 Files](https://github.com/{{site.class_org.name}}/lab01_data)

You should see a listing of several C++ files. Please copy those files into your local lab01 Github repo directory.

If so, you are ready to move on.

If you don’t see those files, go back through the instructions and make sure you didn’t miss a step. If you still have trouble, ask your TA/tutors for assistance.

It’s now time to use the git-command line tools to perform version control for the files in your git repo. The four essential commands we will be using are:
```
git pull
git add .
git commit -m "Initial version of lab01 files"
git push origin main
```
Go ahead and type them out on a terminal in your git repo directory. The above commands save a snapshot of your code on Github. To check that this was done successfully open a web browser and navigate to your repo on Github. Then check to see that the starter code appears in your repo.

Note: Every time you add a new piece of logic to your code, you should save a snapshot of the latest version of your code by issuing the commands: git add … , git commit … and git push …. All the previous versions will be available to you as well and you have the option of reverting to older versions (We will see how in later labs). As you go through the rest of this lab you will essentially need to use these commands to keep track of the different versions of your code. Note that you should only keep relevant files in your repo - avoid uploading non-important LARGE files in your repo since this may cause errors when making your submission to Gradescope.

Congratulations on integrating git into your workflow!

## Step 2: Understand the Code and Finish car.cpp 
In this lab you will create a comprehensive ‘Car’ class with some descriptive variables, constructor, copy constructor, destructor, overloaded assignment operators, and commonly used methods to manipulate member variables. 

The definition of the ‘Car’ class will be provided to you in the head file ‘car.hpp’. The member variables are all private, and listed below:
```
char*  manufacturer;
char*  model;
uint32_t  zeroToSixtyNs;
float  headonDragCoeff;
uint16_t  horsepower;
DoorKind  backseatDoors;
uint8_t  seatCount;
```
The functionalities of these variables can be easily read from their names. The ‘manufacturer’ and ‘model’ are of the type ‘string’, e.g. manufacturer = ‘Audi\0’ and model = ‘R8\0’, which shall be dynamically managed. ‘zeroToSixtyNs’ is the time taken to accelerate from 0 to 60 mph. There are also ‘headonDragCoeff’, ‘horsepower’, and ‘seatCount’. The ‘backseatDoors’ is of the type enumeration, which can take one of the four values: ‘None = 0’, ‘Hinge = 1’, ‘GullWing = 2’, ‘Sliding = 3’, and its declaration will provide to you in the head file ‘doors.hpp’. 

The descriptions of the functionalities of the public methods are listed below:

* Car()
	* Default constructor. Initialize the pointer type variables with ‘NULL’ and the numerical variables with ‘0’. ‘DoorKind’ variable is also initialized with ‘None’.
* Car(char const* const manufacturerName, char const* const modelName, PerformanceStats perf, uint8_t numSeats, DoorKind backseatDoorDesign)
	* Constructor. Initialize the member variables with specific values.
* Car(Car const& o)
	* Copy constructor. Initialize the member variables with the values in ‘o’.
* ~Car()
	* Destructor. Recycle the memory of variables.
* Car& operator=(Car const& o)
	* Overloaded assignment operator ‘=’. Set the values of the variables in the current object to be those in ‘o’.
* char const* getManufacturer() const
	* Get the string of ‘manufacturer’.
* char const* getModel() const
	* Get the string of ‘model’.
* PerformanceStats getStats() const
	* ‘PerformanceStats’ is a structure given to you in the head file ‘perf.hpp’. It summarizes the three parameters ‘horsepower’, ‘zeroToSixtyNs’, and ‘headonDragCoeff’ together. This method gets their values and returns as the structure.
* uint8_t getSeatCount() const
	* Get the number of seats in ‘seatCount’.
* DoorKind getBackseatDoors() const
	* Get the type of the doors in ‘backseatDoors’.
* void manufacturerChange(char const* const newManufacturer)
	* Change the name (string) in ‘manufacturer’ to the new in ‘newManufacturer’. Since the name is of the type string in the memory, please care about the memory management and avoid the memory leak.
* void modelNameChange(char const* const newModelName)
	* Change the name (also string) in ‘model’ to the new in ‘newModelName’.
* void reevaluateStats(PerformanceStats newStats)
	* Update the values of ‘zeroToSixtyNs’, ‘headonDragCoeff’ and ‘horsepower’ by using the new parameters in ‘newStats’.
* void recountSeats(uint8_t newSeatCount)
	* Set the value of ‘seatCount’ to be ‘newSeatCount’.
* void reexamineDoors(DoorKind newDoorKind)
	* Set the kind of the doors in ‘backseatDoors’ to be ‘newDoorKind’.


## Step 3: Test Your Code and Upload to Gradescope
The Autograder will use some test cases to check if your implementations are correct. In order to verify them, you’ll need to write your own test code, which can be a ‘main’ function to print out the results, before the submission. Then, write a Makefile to link all dependencies to make and run your test. 
The lab assignment “Lab01” should appear in your Gradescope dashboard in CS 24. If you haven’t submitted anything for this assignment yet, Gradescope will prompt you to upload your files. For this lab, you will only need to upload your modified file (i.e. car.cpp). 
If you already submitted something on Gradescope, it will take you to their “Autograder Results” page. There is a “Resubmit” button on the bottom right that will allow you to update the files for your submission.
For this lab, if everything is correct, you’ll see a successful submission passing all of the Autograder tests.

**Remember to add your partner to Groups Members for this submission on Gradescope if applicable. At this point, if you worked in a pair, it is a good idea for both partners to log into Gradescope and check if you can see the uploaded files for Lab01.**

