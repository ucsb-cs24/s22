---
title: "Syllabus"
layout: default
ready: true
---

# Syllabus <a name="syllabus"></a>

This document and others linked within it should be your PRIMARY source for understanding the expectations of this course. Be sure to read it *carefully*.
You must contact the instructor for clarification if you receive information from any another source that is in contradiction to what is provided below.

## Basic Facts

* **Course Web Site**: <{{ site.url}}>
* **Instructor**:  {{site.instructor}}
* **Lecture**: {{ site.lecture_times}}, {{ site.lecture_location}} ATTENDANCE HIGHLY RECOMMENDED
* **TAs**: {{ site.tas}}
* **ULAs**: {{site.ulas}}
* **Lab** (50 minute closed lab sections), {{ site.lab_times}}  If you have a section conflict you may informally switch your section time with another student and consistently attend the new time. If you are working with a pair partner, you may attend any section that works for both of you. No need to email the instructor. Section attendance is highly recommended because that's the time when LAs and TAs are available to help you. There is an expectation that you start working on each lab/programmming assignment during sections and use office hours as extra help. 

Please check Gauchospace for staff office hours and Zoom meeting links for lecture, discussion, and office hours.

# Resources

## Required Resources

* Required textbook: E-textbook (Zybook), title: CMPSC 24: Problem Solving With Computers - 2. Instructions to subscribe are on Gauchospace

* Reference textbooks
  * Michael Main and Walter Savitch. Data Structures and Other Objects Using C++ (4th edition), Addison-Wesley, 2011.
  * Problem Solving with C++, Walter Savitch, Edition 10 (edition 9 also works). Available for purchase at the UCSB book store



## What you should know to be ready for CS24

Here's the  list of a few important things you'll need to know to be ready for CS24.

* A few of the basic data types of C++, including at least, int, double, char, bool, string
* The basic control structures of C++ (if/else, while, for etc.)
* Defining functions in C++, and passing parameters to functions in three different ways (by value, by pointer, and by reference)
* Scope and lifetime of variables in C++
* The use of "const" with parameters to functions
* Using arrays in C++, and C-strings (null-terminated character arrays)
* Defining and working with structs and classes in C++
* Converting from binary to decimal, octal, and hex, and back again&mdash;and how this relates to how C++ programs store various kinds of data in memory.
* The basic principles of recursion, and some idea of when a recursive solution is appropriate.

# Course objectives

* Learn about the C++ Memory Model and Dynamic Memory allocation 
* Learn about the difference between space allocated on the stack (e.g. local variables) and space allocated on the heap (with the new and delete operators)
* Learn object-based programming techniques: abstraction and encapsulation.
* Learn to specify, implement and apply lists, trees and other data structures using OOP principles.
* Learn to distinguish algorithms and data structures on the basis of efficiency by analyzing their complexity (Big-Oh).
* Learn (and practice) to produce better programs more quickly and with less stress.


# Grade Breakdown

Grades in this class are designed to reflect your work and to document evidence of your learning core material. The graded components for CS24 are described below:


* Zybook activities: 15%. Note: There are two types of activities in the book: participation and challenge. The "participation activities" are graded for attempt only. The "challenge activities" are graded for correctness. However, you can try them as many times as you like without penalty. They are more like mini autograded home works. An orange check mark will appear on the top right corner of the activity after you complete each activity. 
Note: If purchasing the book imposes a financial hardship that you cannot bear, please contact lori.berns@zybooks.com for assistance. Alternatively, you may choose not to purchase the subscription if you are an advanced C++ programmer and have a solid understanding of data structures and complexity analysis of algorithms. In this case, your grade for this component will be replaced by the average of your midterm and final exam scores.

* Weekly lab assignments: 15%. These provide regular practice in preparation for larger and more complex programming assignments. Check the instructions on top of each assignment for collaboration policy. Some assignments may be completed in pairs. 

* Programming assignments: 20%. Check the instructions on top of each assignment for collaboration policy. Some assignments may be completed in pairs. 

* Midterm: 15% of overall score. 

* Final Exam: 35% of overall score. 


## Timeliness on assignments

Each lab, programming assignment, zybook reading asssignment has two deadlines: (1) The "on-time" deadline which is the one published on the course calendar. Submitting by this deadline gets you a timeliness bonus of 1% (of the assignment score) 
(2) The "late" deadline which is 4 days after the published deadline. You will not be penalized for submitting before this deadline but doing so would mean that you don't get the timeliness bonus.

We will not accept submmissions past the second deadline.

You are responsible to make sure you have the correct score for your assignments prior to the due date. This is specially important if you are working with a programming partner.

## Academic Integrity

Please read about actions that are categorized as Academic Dishonesty on the UC Santa Barbara Office of Student Conduct website:
<http://studentconduct.sa.ucsb.edu/academic-integrity>

Academic integrity violations will be taken seriously, reported to the campus-wide Office of Student Conduct, and will result in either lowering your grade by a whole grade point or an F in the course. Key facts about academic integrity related to CS24:

* Using or attempting to use materials, information, study aids, or commercial “research” services not authorized by the instructor of the course constitutes cheating.
* Representing the words, ideas, or concepts of another person without appropriate attribution is plagiarism. 
* Whenever another person’s written work is utilized, whether it be a single phrase or longer, quotation marks must be used and sources cited. Paraphrasing another’s work, i.e., borrowing the ideas or concepts and putting them into one’s “own” words, must also be acknowledged. If you refer to any information through a websearch for programming assignments, cite the source in your solution.
* Do not publicly post any component of the graded components in this class (such as book activities, labs, programming assignments, quizzes and exams) or solicit answers from sources that are not explicitly allowed for each assignment.
* Ensure that the visibility of your git repositories are private.
* Do not share partial or complete solutions for programming assignments or labs with other students in the class who are not in your group. 
* Before and during taking any individual assessment, do not attempt to obtain information about the contents of the exam from students who have already taken it or from any nonauthorized sources (Chegg, stack overflow, or any other paid tutoring service).
* You may not ask for help from anyone while taking individual assessments since they are intended to reflect your own mastery of the material. In particular, you may not collaborate on quiz/exam questions with other students in the class and you may not post any portion of the quiz/exam on forums where others may assist you.
* After taking an exam or quiz, do not discuss its contents with anyone in the class who has not yet taken it. Do not post information about it or share information about it with others who haven't taken it.
* If working with a pair partner on assignments, add the name of your partner to the assignment on Gradescope and only submit one version.
* Follow pair programming guidelines when collaborating on programming assignments. Pair programming on an assignment does not mean that you can simply divide the work for the assignment, rather you are expected to code together following pair programming guidelines. 



### About Collaboration

As mentioned above, one of the things we really want to convey in this course is that real-world software development is very seldom an 'individual sport'—it is much more often a 'team sport'. Companies want to hire CS and CE graduates that know how to collaborate with others on producing software.

In the CS Department at UCSB, we understand the value of this. However, it puts us in a tricky position. On the one hand, we want to encourage working together in ways that help you develop your skills and teamwork, and help you understand that programming can be a social, collaborative, creative activity—not something done only by loner nerds in cubicles. The sooner you start with activities such as pair programming, code reviews, and other collaborative software development activities, the more skill you'll develop, and the sooner you'll be ready for the real world. Plus, for many people, working together with others is a lot more enjoyable and fun than being a loner.

On the other hand, we need to avoid any situations where freeloaders are &quot;coasting&quot; through courses by leaning too much on others—never developing independent skills as programmers. This situation creates huge problems. Mostly it is damaging to the freeloaders themselves, who eventually crash and burn, perhaps far too late to choose another career path without significant difficulty. However, it also creates problems for everyone else—some hardworking students become demoralized by the unfairness of it all, and the value of a UCSB education is diminished by the  freeloaders' lack of accomplishment.
Thus, we must strike a balance. 
Our emphasis on collaboration means:
* We will try to create opportunities for you to work in pairs on assignments—in some cases, we may even require it.
* We will try to create opportunities for you to develop the ability to think critically about software development by talking about and reflecting on your own code and other people's code in small groups.
* Some in-class assignments will permit discussion with other students.
However: 
  * You may not &quot;just copy&quot; homework or code from others and claim it as your own work.
  * You may not work together on assignments unless you've been specifically told that it is allowed.

A final note:  the emphasis on collaboration in this course does not necessarily extend to other CS courses you may take in the future.

  * Each course will have its own policies, and the default policy is still: <strong>no collaboration.</strong>
  * Please be sure you understand each instructor's policy on collaboration carefully, and don't assume it will be the same as that from previous courses.
  * And, finally, be sure to review the UCSB Academic Honesty Policy. You should read and understand the UCSB policy on academic honesty listed below. You should also understand that I take academic honesty and personal integrity very seriously, and will do my best to uphold and enforce this UCSB policy.


## About pair programming

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


## Makeups for exams

* Makeups on exams will only be given if there is an emergency situation that you could not predict or avoid including but not limited to major illness

* No makeups will be given if you have a conflict with any of the exams for this course. Please check for conflicts with the final!


## Disabled Students Program (DSP)
UCSB provides academic accommodations to students with disabilities. Students with disabilities are responsible for ensuring that the Disabled Students Program (DSP) is aware of their disabilities and for providing DSP with appropriate documentation. DSP is located at 2120 Student Resource Building and serves as the campus liaison regarding issues and regulations related to students with disabilities. The
DSP staff works in an advisory capacity with a variety of campus departments to ensure that equal access is provided to all disabled students.
If you have a disability that requires accommodation in this class, please go see the DSP very early on in the quarter. I will only honor these types of requests for accommodation via the DSP. More information about the DSP is found here: [http://dsp.sa.ucsb.edu](http://dsp.sa.ucsb.edu)





## Disclaimer
The course policies have been provided as accurately as possible, but are subject to change at the instructor's discretion, within the bounds of UC policy.



[Back to Syllabus](#syllabus){: data-ajax="false"}
