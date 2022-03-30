---
layout: lab
num: lab00
ready: true
desc: "Getting started"
assigned: 2022-03-31 15:00:00.00-8
due: 2022-04-04 23:59:00.00-8
---


# Introduction

Your first lab for this week is an introduction to programming on CSIL and tools for this course. The intended outcomes are:

* Get to know the course staff and help us get to know you
* Learn about the tools you will be using in this class: gradescope and github
* Find a partner for lab01

This lab will count towards 2% of your total lab grade. All other labs are weighed equally.

This lab must be completed INDIVIDUALLY. In the subsequent labs you are encouraged to work with your programming partner.
 

# Get setup with the tools for this course

## Create a CoE account if you don't have one already

We encourage you to complete all programming assignments by logging in to the machines in the Computer Science labs, or to connect remotely. To do this you will need a **College of Engineering account**. You can create an account online at <a href="https://accounts.engr.ucsb.edu/create" target="_blank">https://accounts.engr.ucsb.edu/create</a>.

If you are enrolled in <i>any</i> CoE course this quarter (including CS24), you can create your account immediately. If you are not, you will need to contact the ECI Help Desk at <a href="mailto:help@engineering.ucsb.edu">help@engineering.ucsb.edu</a>.

## Get setup with github

We will be using github.com in this course.   We have created an organization called {{site.class_org.name}} on github.com where you can create repositories (repos) for your assignments in this course.   The advantage of creating private repos under that organization is that the course staff (your instructors, TAs and mentors) will be able to see your code and provide you with help, without you having to do anything special.

To join this organization, you need to do three things.

1. If you don't already have a github.com account, create one on the "free" plan. Visit [www.github.com](https://github.com/)

2. If you don't already have your @umail.ucsb.edu email address associated with your github.com account. go to "settings", add that email, and confirm that email address.

3. Visit our [Github Sign Up Tool: https://ucsb-cs-github-linker.herokuapp.com/](https://ucsb-cs-github-linker.herokuapp.com/), login with your github.com account, click "Home", find this course ({{site.org.githublinker}}), and click the "join course button".   That will automatically send you an invitation to join the course organization on github. 

4. Accept the invitation that appears in your browser (from step 3) or log into your account on [www.github.com](https://github.com/) to accept the invitation.

## Get setup with gradescope

We will use gradescope to grade all your homeworks, exams and lab/programming assignments. You should have received an email notification with instructions about logging into gradescope.

Log into our class site on [www.gradescope.com](https://www.gradescope.com/): {{site.name}}    and navigate to the lab00 assignment

# Implement and submit a simple C++ program 

## Download and install VSCode on your local computer

Download and VSCode at this link: <https://code.visualstudio.com/download>

If you have MAC OS or Linux with g++ installed, skip to Step 1A below

If you have a Windows system and don't have a g++ compiler, follow this tutorial to use your local version of VSCode with the g++ compiler on the CSIL Servers: <https://code.visualstudio.com/docs/remote/ssh-tutorial>

If you would like to use vim or emacs instead of VSCode follow the instructions in the next section.

## Open a Terminal and ssh into CSIL Servers

Open a **terminal window**, which will be the environment you use to write, compile, and run your programs.

If you are working on your laptop, whether Windows, Mac or Linux, the instructions below will tell you how to connect to `csil.cs.ucsb.edu`.

If you are on a Mac laptop, open a terminal and type the 
following ssh command to connect to one of the servers remotely

```
ssh -X yourCoEaccount@csil.cs.ucsb.edu
```
If you are using a Windows, you will need to install the program
[MobaXterm](https://mobaxterm.mobatek.net/)
If your ssh command is hanging, try using `cstl.cs.ucsb.edu` with the following command

```
ssh -X yourCoEaccount@cstl.cs.ucsb.edu
```

## Step 1a: Do some initial ONE-TIME git configurations

To create your CS24 directory, use the <b>mkdir</b> command, then change into that directory:

```
$ mkdir cs24
$ cd cs24
```
* In your ~/cs24 directory, type the following commands, replacing Alex Triton with your name and atriton@cs.ucsb.edu with your email address.

```
git config --global user.name "Alex Triton"

git config --global user.email "atriton@cs.ucsb.edu"
```

* Next, generate a private/public key pair and upload your public key to your github account. Refer to this tutorial: [https://ucsb-cs56-pconrad.github.io/topics/github_ssh_keys/](https://ucsb-cs56-pconrad.github.io/topics/github_ssh_keys/). In the process of setting up your key pair, when asked for a passphrase **just press enter**. By doing this step you will avoid having to enter a password or passphrase everytime you push your code to git.


## Step 1b: Create a new repo and clone it on your local machine
For this lab and all subsequent programming assignments, you should start by creating a repo in the {{site.class_org.name}} organization following these steps

* Navigate to your dashboard on [https://github.com](https://github.com). From the left drop down menu, select the class organization as shown in the figure below:
![select-org](select-org.png){:height="500px"}

* Click on the green "New repository" button to create a new repository.

* Type the name of your repo following the naming convention lab00_your-github-username. For example if your github username is jgaucho, you should name your repo as lab00_jgaucho. If you are working with a partner, include your partner's github username in the name of the repo. e.g. lab00_jgaucho_alily

* Select the "Private" visibility option so that other students in the org cannot view your code.

* Add the C++ .ignore option from the frop down menu and click on "Create repository". See screenshot below.

![new-repo](enter-org/pic5.png){:height="500px"}

* Clone the repo on your local machine: Navigate to your repo on github. If your repo is named lab00_jgaucho, then you have to go to to the link:
https://github.com/{{site.class_org.name}}/lab00_jgaucho. Click on the green "clone or download" button. Then click on the address of your repo as shown in the figure below:

![submit](/lab/lab01/clone-repo.png){:height="500px"}

* In your cs24 directory, then paste the address you just copied to the terminal following the git clone command. Here is an example of the steps

```
git clone git@github.com:{{site.class_org.name}}/lab00_jgaucho.git
```

* The above command will create a new directory with the same name as your git repo. Change into that directory. For our example repo we need to type

```
cd lab00_jgaucho
```

You will write all the code for this assignment in this directory

## Step 1c: Complete the assignment

Create a new file called <code>hello.cpp</code> using an editor of your choice (either vim or emacs)

Useful links related to emacs

* <a href="https://www.gnu.org/software/emacs/tour/" target="_blank">emacs tour from the GNU organization (makers of emacs)</a>

* <a href="https://www.gnu.org/software/emacs/refcards/pdf/refcard.pdf" target="_blank">emacs commands - a handy reference card</a>

* <a href="http://www.jesshamrick.com/2012/09/10/absolute-beginners-guide-to-emacs" target="_blank">a beginner's guide to emacs</a>

Useful information related to <b>vim</b> for UNIX-based OS

* To customize your vim environment for a better coding experience with C/C++ copy this .vimrc file from the instructor folder to your home folder using the following command:

```
cp /cs/faculty/dimirza/vim-configuration/example_dotvimrc/.vimrc ~/
```

* <a href="http://www.vim.org/about.php" target="_blank">About vim</a>

* <a href="http://tnerual.eriogerg.free.fr/vimqrc.html" target="_blank">vim commands - a handy reference card</a>

* <a href="https://www.fprintf.net/vimCheatSheet.html" target="_blank">another reference cheat sheet for vim</a>

This assignment only needs you to write a program in hello.cpp that prints out two lines on the display, and nothing else. **The output should look exactly as follows** (no space before or after each line, except the 2 newlines):

```
Hello, world!
I am ready for CS24!
```

## Step 1d: Push your code to github

In furture labs we will refer to all the steps in this section as "push your code to github". What we really mean is that you sync up a current version of your code with your repo on https://github.com. Follow these steps to sync the current version of your code:

* Check the status of the files that changed since the last time you synced your repo. Just type git status as follows:

```
git status
```

You should see the following output:

```
On branch main
Your branch is up to date with 'origin/main'.

Untracked files:
(use "git add ..." to include in what will be committed)

hello.cpp

nothing added to commit but untracked files present (use "git add" to track)
```

* Now add the files that were modified since the last sync using git add

```
git add hello.cpp
```
OR

```
git add .
```

Type git status again and you should see that the file appears in green. This means it is ready to be "saved" locally as a new version of your project.

* Save the current version of your code as follows:

```
git commit -m "Initial version of lab00"
```

* Finally sync your latest changes with your repo on https://github.com using git push

```
git push origin main
```

Navigate to your repo and refresh your browser. You should see the new file that you added to your repo appear in your repo online.
You may find this [cheatsheet of git commands](https://education.github.com/git-cheat-sheet-education.pdf) handy.

**Your code is now accessible to the CS24 teaching staff for feedback.** This is the primary reason we are using github in this class. As you write new code in your local repo, repeat the steps in this section to sync your changes with your repo on github.

## Submit your program for grading to gradescope

It's time to submit your program to gradescope. Go to [www.gradescope.com](https://www.gradescope.com/). Log into your account and navigate to our course site. Select this assignment. Then click on the "Submit" button on the bottom right corner to make a submission.

You will be given the option of directly uploading files from your local machine or submitting the code that is in a github repo. We recommend that you choose the latter option as shown in the figure below. This will ensure that our staff sees the version of code on github that you submitted to gradescope.

![submit](enter-org/gradescope-submission.png){:height="500px"}

You should receive 50 points on this part of the assignment.

Congratulations on completing the workflow for CS24 programming assignments using the tools that we will be using in this class i.e. gradescope and github. 

# Find a partner for lab01

## About pair programming in the real world

*Note: this is also in the syllabus!*

Most of the programming work in this course will be done using a style of programming known as &quot;pair programming&quot;. This is where two people (in rare cases, three) work together at the same terminal to solve a programming problem.
It is similar, in some ways, to having a &quot;lab partner&quot; in a Biology, Chemistry or Physics course.
For the assignments where pair programming is mentioned, it is optional. But here's why we recommend it:
* Pair programming is a real-world skill that is highly valued by employers.
* Many companies use pair programming extensively, including several local area employers of UCSB CS graduates.
* Companies that employ UCSB CS and CE grads tell us that our graduates have good technical skills but need better skills and working in pairs and groups to solve problems.
* Incorporating  pair programming into our curriculum is part of our response to this &quot;real-world&quot; feedback.
* Most students find it helpful and enjoyable—UCSB CS students from 2009-2010 that were surveyed about their pair programming experiences overwhelmingly reported positive results.
* There is also evidence in the scientific literature that it improves student learning, and helps you get better grades.
* To learn more about pair programming, watch the following video (it takes less than 10 minutes): [http://bit.ly/pair-programming-video](http://bit.ly/pair-programming-video)

## About pair programming in CS24 

For CS24 in particular, **please read each lab carefully to learn how pair programming will work for that lab**. Some labs may require you to work by yourself, others may require you to work with a partner, and still others may allow you to do either. In addition, some labs may allow you to work with a prior partner, while others may not. 

For all labs, you MUST
* add your partner on Gradescope when submitting your work EACH TIME you submit your file(s). After uploading your file(s) on Gradescope, there is a “Group Members” link at the bottom (or “Add Group Member” under “Groups”) where you can select the partner you are working with. Whoever uploaded the submission must make sure your partner is part of your Group. Click on “Group Members” -> “Add Member” and select your partner from the list.
* write both your and your partner's names and PERM numbers on each file submitted to Gradescope.

## Fill out the partner assignment form for lab01

Please fill out [this partner assignment form](https://forms.gle/mG63Ja34CTZWjzZT9) before you begin working on lab01.

* If you already have a partner, then please fill out this form now.
* If you don't have a partner, and you want to be assigned one, then please fill out this form now. The TAs will assign you a partner based on some info about yourself.
* If you don't have a partner, and you want to search for one, then please use the dedicated Piazza thread called [Search for Teammates](https://piazza.com/class/l142oiw36ef1gh?cid=5) (this will help us avoid clutter on Piazza). After you find a partner, fill out this form.