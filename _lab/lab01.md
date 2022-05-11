---
layout: lab
num: lab01
ready: true
desc: "Linked Lists in C++ with structs"
assigned: 2022-04-06 15:00:00.00-8
due: 2022-04-13 23:59:00.00-8
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

Before you create your repo, we'll introduce 2 different methods for you to set up the starter code in your own repo.   

### Method A: Add starter code repo as a new Git remote

Most of the instructions for this method is adopted from <https://ucsb-cs16.github.io/w22/lab/lab03/>

#### Step A1: Create your lab01 repo on GitHub

Create an empty repo on GitHub under the name `lab01-YOUR-GITHUB-ID-PARTNER-GITHUB-ID`. You **must uncheck** the options for creating `README.md` and `.gitignore` files when you create your repo to keep it empty.     

Following the steps outlined in lab00, use the SSH address to clone this repo onto your local machine through command line, i.e.

```
git clone git@github.com:ucsb-cs24-s22/lab01-YOUR-GITHUB-ID-PARTNER-GITHUB-ID.git
```

After that, you should have a local directory called `lab01-YOUR-GITHUB-ID-PARTNER-GITHUB-ID`.   
Use the `cd` command to move into this directory.

You may want to practice moving between this directory and the parent directory a few times, and using the `ls` and `pwd` commands to understandwhat is happening   
`cd ..` lets you move into the parent directory   
`pwd` lets you print the path of your current working directory (hence, `p`rint `w`orking `d`irectory)   
`ls` lets you list the content of the directory   

You can use `ls -a` to see that while the directory may appear empty, there is a hidden folder called `.git` that marks this folder as a git repository (or repo for short) in the local repo you just cloned:

```
$ ls -a
.  ..  .git
$
```

#### Step A2: Create the `main` branch in your repo

Every git repo can have multiple *branches* of code; this is useful on  projects where there are multiple programmers collaborating on a solution.  Multiple branches allow for
different versions of the code to live side-by-side in a repository, and then be merged together at a later stage.

* Courses that involve group work (such as CMPSC 148 and/or CMPSC 156) may cover the use of git with multiple branches.
* However, in this course, to keep things simple, **we'll typically stick to just one branch** 

This single branch is sometimes called the *default branch*.
* Prior to October 1, 2020, the usual name for that branch was `master`.
* Starting October 1, 2020, GitHub started calling the default branch `main`

Not all `git` software is updated with this convention however.  Accordingly, when we clone a new repo, to align our local repo with GitHub,
our first step is to set the current branch to `main` by running the following command in your local repo:

```
git checkout -b main
```

The `git checkout` command is the one that is used to switch from one branch to another, and the `-b` command says that we are creating a new
branch in our local repo.

For the time being, and probably throughout CS24, this is likely everything you need to know about branches (at least for the purposes of this course.)

Now we are ready to pull in some starter code.

#### Step A3: Add a remote for starter code.

While in your local repo, type this command:

```
git remote -v
```

The `-v` here stands for `verbose`, and it means that the command will give lots of helpful information. The output should look like this:

```
$ git remote -v
origin	git@github.com:ucsb-cs24-s22/lab01-YOUR-GITHUB-ID-PARTNER-GITHUB-ID.git (fetch)
origin	git@github.com:ucsb-cs24-s22/lab03-YOUR-GITHUB-ID-PARTNER-GITHUB-ID.git (push)
$ 
```

Explanation:
* The word *remote* refers to a Git repo that lives on some other computer; in this case, a GitHub.com server. 
* The output above shows that you have one *remote* called `origin` and it shows the URL associated with that name `origin`.  
* By convention, the name `origin` is used for the GitHub repo from which you cloned the current repo, i.e. the one that came after `git clone` in a previous step.

What we are doing to do next is add a second remote, called `starter`.  From this remote, you'll be able to pull in some starter code; your lab solution will involve
working with some of that starter code.

The starter code lives in this repo, which you can visit in a web browser to look at the starter code:
* <https://github.com/ucsb-cs24-s22/STARTER-lab01>

To add a remote for this repo, we'll use the ssh url, like this:

```
git remote add starter git@github.com:ucsb-cs24-s22/STARTER-lab01.git
```

To see if it worked, you can type the `git remote -v` command again. Output should look like this (with YOUR-GITHUB-ID replaced by your github id. 

```
$ git remote -v
origin	git@github.com:ucsb-cs24-s22/lab01-YOUR-GITHUB-ID-PARTNER-GITHUB-ID.git (fetch)
origin	git@github.com:ucsb-cs24-s22/lab03-YOUR-GITHUB-ID-PARTNER-GITHUB-ID.git (push)
starter	git@github.com:ucsb-cs24-s22/STARTER-lab01.git (fetch)
starter	git@github.com:ucsb-cs24-s22/STARTER-lab01.git (push)
$ 
```

Note that if the URLs are wrong for either the `origin` or the `starter` remotes, you can fix that by doing this command to remove a remote:
* `git remote remove origin` to remove the remote `origin`
* `git remote remove starter` to remove the remote `starter`

Then you can add the remote back with the correct URL, e.g.:
* `git remote add origin git@github.com:ucsb-cs24-s22/lab01-YOUR-GITHUB-ID-PARTNER-GITHUB-ID.git`
* `git remote add starter git@github.com:ucsb-cs24-s22/STARTER-lab01.git`

This can be used, for example, if you accidently cloned the repo using the `https` url instead of the one that starts with `git@github.com` (which is the SSH based URL).

Assuming your remote for `starter` is now set up correctly, the next step is to pull in the starter code.

#### Step A4: Pull in Starter Code

To pull in the starter code, use:

```
git pull starter main
```

Then use an `ls` command, and you should see new files in your directory.  That should look something like this:

```
$ ls
$ git pull starter main
remote: Enumerating objects: 10, done.
remote: Counting objects: 100% (10/10), done.
remote: Compressing objects: 100% (7/7), done.
remote: Total 10 (delta 2), reused 7 (delta 2), pack-reused 0
Unpacking objects: 100% (10/10), 2.45 KiB | 47.00 KiB/s, done.
From github.com:ucsb-cs24-s22/STARTER-lab01
 * branch            main       -> FETCH_HEAD
 * [new branch]      main       -> starter/main
$ 
```

With these files in place, you are ready to start coding.

If you don't see those files, go back through the instructions and make sure you didn't miss a step.

### Method B: Clone starter code repo in a separate location and copy the files

#### Step B1: Create and clone your lab01 repo

Create a repo on GitHub under the name `lab01-YOUR-GITHUB-ID-PARTNER-GITHUB-ID`. You can check the option for creating a `README.md` so that your new repo is non-empty. You should check the option to create a `.gitignore` and select C++ as the language so that Git will only track your cpp files and makefile and ignore any object files (`.o` files) and executables.     

Following the steps outlined in lab00, use the SSH address to clone this repo onto your local machine through command line, i.e.

```
git clone git@github.com:ucsb-cs24-s22/lab01-YOUR-GITHUB-ID-PARTNER-GITHUB-ID.git
```

### Step B2: Clone the starter code repo

The starter code is in this repo:
* <https://github.com/ucsb-cs24-s22/STARTER-lab01>
* The SSH link for this repo is: `git@github.com:ucsb-cs24-s22/STARTER-lab01.git`

Clone the starter code repo through the ssh link **outside of** your lab01 repo.   
We want to avoid nesting git repositories within one another.

### Step B3: Copy the starter code files into your repository

Assuming that you your starter code repo and lab01 repo are located in the same directory, e.g. `~/cs24` (note that `~` is the symbol for root directory)   so that your directory structure looks something like this:
```
$ cd ~/cs24
$ ls
lab01-YOUR-GITHUB-ID-PARTNER-GITHUB-ID      STARTER-lab01      <some other files or directories>
```

Now we can use the `cp` command to copy files from `STARTER-lab01` into `lab01-YOUR-GITHUB-ID-PARTNER-GITHUB-ID`   
Note that the syntax for the `cp` command looks like this:
```
cp <path_of_file_to_copy> <destination_to_copy_to>
```
So for our purpose, we will run the following command:
```
cp STARTER-lab01/* lab01-YOUR-GITHUB-ID-PARTNER-GITHUB-ID/
```
We use the symbole `*` to indicate we want to copy all files from `STARTER-lab01`   

`cd` into your lab01 repo to make sure all of the files are copied
```
cd lab01-YOUR-GITHUB-ID-PARTNER-GITHUB-ID
```

You may want to practice moving between this directory and the parent directory a few times, and using the `ls` and `pwd` commands to understandwhat is happening   
`cd ..` lets you move into the parent directory   
`pwd` lets you print the path of your current working directory (hence, `p`rint `w`orking `d`irectory)   
`ls` lets you list the content of the directory   

## Step 2: Checking that your lab01 repo has all starter code files

Once you've pulled or copied the started code into your lab01 repo, typing the `ls` command on your machine should show you the following files in your current directory

```
$ ls
Makefile              linkedListFuncs.h	       tddFuncs.cpp
README.md             llTests.cpp		           tddFuncs.h
linkedList.h          moreLinkedListFuncs.cpp
linkedListFuncs.cpp	  moreLinkedListFuncs.h
```

Now add the changes with the starter code files, make an initial commit in your local repository, and push the new commit to your remote repository
```
git add .
git commit -m "Initial version of lab01 files"
git push origin main
```
If the push succeeds, you should see that your remote repository on GitHub is now updated with all the starter code files, and you are ready to get started with coding the lab.   

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

## Fill out the partner assignment form for lab02

Please fill out [this partner assignment form](https://forms.gle/AeMahHqPy243FQtX8) before you begin working on lab02.

* If you already have a partner, then please fill out this form now.
* If you don't have a partner, and you want to be assigned one, then please fill out this form now. The TAs will assign you a partner based on some info about yourself.
* If you don't have a partner, and you want to search for one, then please use the dedicated Piazza thread called [Search for Teammates](https://piazza.com/class/l142oiw36ef1gh?cid=5) (this will help us avoid clutter on Piazza). After you find a partner, fill out this form.
* If you wish to work alone, then you do not need to fill out this form
