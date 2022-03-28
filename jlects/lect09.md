---
num: "lect09"
lecture_date: 2021-02-03
desc: "Linked list. Recursion."
ready: true
annotatedready: false
---
## Relevant topics in the textbook:
Data Structures and Other Objects Using C++ Chapter 5 and Chapter 9

# Linked List Implementation

```
// LinkedList.h
#ifndef LINKEDLIST_H
#define LINKEDLIST_H

struct Node {
	int data;
	Node* next;
};

struct LinkedList {
	Node* head;
	Node* tail;
};

void printList(LinkedList* list);
void insertToFront(LinkedList* list, int value);
bool exists(LinkedList* list, int value);
int length(LinkedList* list);
void deleteIndex(LinkedList* list, int index);

#endif
--------------
// LinkedList.cpp
#include <iostream>
#include "LinkedList.h"
using namespace std;

void printList(LinkedList* list) {
	for (Node* i = list->head; i != NULL; i = i->next) {
		cout << "[" << i->data << "]->";
	}
	cout << "null" << endl;
}

void insertToFront(LinkedList* list, int value) {
	if (list->head == 0) {		// empty list
		Node* item = new Node;
		item->data = value;
		item->next = NULL;
		list->head = item;
		list->tail = item;
	} else { 			// not empty
		Node* item = new Node;
		item->data = value;
		item->next = list->head;
		list->head = item;
	}
}

bool exists(LinkedList* list, int value) {
	for (Node* i = list->head; i != NULL; i = i->next) {
		if (i->data == value)
			return true;
	}
	return false;
}

int length(LinkedList* list) {
	int counter = 0;
	// let's use a while loop instead of a for...
	Node* temp = list->head;
	while (temp != 0) {
		counter++;
		temp = temp->next;
	}
	return counter;
}

void deleteIndex(LinkedList* list, int index) {
	if (index >= length(list) || index < 0) {
		cerr << "Invalid index: " << index << endl;
		return;
	}

	// check if first item
	if (index == 0 && list->head != 0) {
		Node* temp = list->head;
		list->head = list->head->next;
		delete temp;
		return;
	}

	Node* prev = list->head;
	Node* curr = list->head->next;
	for (int i = 1; i < index; i++) {
		prev = prev->next;
		curr = curr->next;
	}

	// remove the current node
	prev->next = curr->next;
	delete curr;

	// re-assign list->tail if curr was the last node.
	if (index == length(list))
		list->tail = prev;

	return;
}
----------
// main.cpp
#include <iostream>
#include <string>
#include <fstream>
#include "LinkedList.h"

using namespace std;

int main() {
	LinkedList* list = new LinkedList;
	list->head = 0;
	list->tail = 0;

	cout << length(list) << endl;

	insertToFront(list, 10);
	cout << length(list) << endl;
	insertToFront(list, 20);
	insertToFront(list, 30);
	printList(list);			// 30->20->10

	cout << exists(list, 15) << endl; 	// 0
	cout << exists(list, 30) << endl; 	// 1
	cout << exists(list, -1) << endl; 	// 0

	cout << length(list) << endl;		// 3

	deleteIndex(list, -1); 			// err
	deleteIndex(list, 5);			// err
	deleteIndex(list, 3);			// err
	deleteIndex(list, 2);			// OK!
	printList(list);			// 30->20->null

	return 0;
}
----------
$ g++ -o main main.cpp LinkedList.cpp
```

# Recursion

* When a function contains a call to itself.
* We’re mostly familiar with writing code in an iterative fashion (i.e. one statement after the other).
	* Several programming languages exist where it’s based purely on recursion.
* Useful for problems that can be solved by using the results of similar sub problems.

## Properties of Recursion
* One or more base cases that providing the "stopping" condition
* One or more recursive calls, where the arguments are "closer" to the base case than the function input.
* Any recursive function can be done in an iterative way and any iterative function can be done in a recursive way.

## Example: Factorial

* N! = N * (N-1) * (N-2) * ... * 3 * 2 * 1
	* Note: 0! = 1, 1! = 1

```
int factorial (int n) {
	if (n==0) return 1;
	
	return n*factorial(n-1);
}
---
int main() {
	cout << factorial(4) << endl; // 24	
}

```

* Evaluation of factorial(4)

```
factorial(4) = 4 * factorial(3)
                   3 * factorial(2)
                       2 * factorial(1)
                           1
                       2 * 1
                   3 * 2
               4 * 6
               24
```

## Example: Fibonacci

* A fibonacci sequence is when nth number in the sequence is the sum of the previous two (i.e. f(n) = f(n-1) + f(n-2)).
* f(n) = f(n-1) + f(n-2))
* f(0) = 0, f(1) = 1, f(2) = 1, f(3) = 2, f(4) = 3, f(5) = 5, f(6) = 8, … , f(n) = f(n-2) + f(n-1)

```
int fibonacci(int n) {
	if (n==1) return 1;
	if (n==0) return 0;
	return fibonacci(n-1) + fibonacci(n-2);
}
-----
int main() {
	cout << fibonacci(4) << endl; 3
}
```

* Evaluation of fibonacci(4)

```
fib(4)
fib(2)          + fib(3)
fib(0) + fib(1) + fib(3)
0      + 1      + fib(3)
1               + fib(1) + fib(2)
1               + 1      + fib(2)
1               + 1      + fib(0) + fib(1)
1               + 1      + 0      + 1
3
```

## Example: Recursively find the length of a C-string

```
int recLength(char* s) {
	char temp = *s;

	if (temp != '\0') {
		return 1 + recLength(&s[1]);
	} else {
		return 0;
	}
}
----
char s1[] = {'a', '\0'};
char s2[] = {'\0'};
char s3[] = {'a', 'a', 'a', '\0'};

cout << recLength(s1) << endl;
cout << recLength(s2) << endl;
cout << recLength(s3) << endl;
```

## Recursion Performance

* Recursion consumes more memory than an iterative solution since it keeps adding memory to the call stack.
* Recursion can sometimes be simply written vs an iterative algorithm (more readable).

## Stack Overflow

* An event that happens when a program crashes due to running out of memory in its call stack.
	* Usually happens when there is an infinite loop of recursive calls.
	* For example, forgetting to provide a base case may result in an infinite number of recursive calls.

```
int factorial (int n) {
/* REMOVE BASE CASE
	if (n == 1) // base case
		return 1;
*/

	cout << n << endl;
	return n * factorial(n – 1);
}
```
