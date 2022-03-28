---
num: "lect05"
lecture_date: 2021-01-20
desc: "The Big Three"
ready: true
annotatedready: false
---
## Relevant topics in the textbook:
Data Structures and Other Objects Using C++ Chapter 2.1, 2.2, 2.5

# Classes

* Classes are a representation of a custom-defined type.
* Classes consist of:
	* An <i>interface</i>: What operations and variables are available when using this class.
	* An <i>implementation</i>: The definition of how things are done.

## A note about C++ structs

* structs and classes in C++ are <b>exactly</b> the same except for the following:
    * Struct members are set to <b>public</b> by default.
    * Class members are set to <b>private</b> by default.

## Example - definition of a class representing a Person

```
# Makefile

CXX=g++
DEPENDENCIES=main.o Person.o

main: ${DEPENDENCIES}
	${CXX} -o $@ -std=c++11 $^

clean:
	rm -f *.o main
```

```
// Person.h
#ifndef PERSON_H
#define PERSON_H

#include <iostream>

// Interface for class representing a Person

class Person {
	public:
		Person(); 				// default constructor
		Person(std::string name, int age);	// overloaded constructor
		Person(Person& person);			// copy constructor
		std::string getName() const; 		// accessor / getter
		int getAge() const; 			// accessor / getter
		void setName(std::string name); 	// mutator / setter
		void setAge(int age);			// mutator / setter

	private:
		std::string name;
		int age;
};

#endif
```

<b>Note:</b> You should not use `using namespace` in your header files. This forces consumers of the class to use the namespace, which may not be intended or expected.

```
// Person.cpp
#include <iostream>
#include <string>
#include "Person.h"

using namespace std;

// default constructor
Person::Person() {
	name = "-";
	age = 0;
	cout << "Default Constructor" << endl;
}

// constructor overloading
Person::Person(string name, int age) {
	this->name = name;
	this->age = age;
}

// copy constructor
Person::Person(Person& person) {
	name = person.getName();
	age = person.getAge();
	cout << "copy constructor" << endl;
}

string Person::getName() const { return name; }

int Person::getAge() const { return age; }

void Person::setName(string name) { this->name = name; }

void Person::setAge(int age) { this->age = age; }
```

```
// main.cpp

#include <iostream>
#include "Person.h"

using namespace std;

int main() {
	Person p;
	return 0;
}
```

## Public vs. Private
* The variables and functions declared as private cannot be referenced anywhere except within the class’ functions.
* The variables and functions declared as public can be referenced anywhere.
	* Why is this good?
		* Prevents unintended side-effects.
		* Hides complex details consumers of the class may not be concerned with.

## Abstract Data Types (ADTs):
* A data type where the programmers who use this class do not have access to the details of how the values and operations are implemented.
	* Also known as data hiding, data abstraction, and encapsulation.
	* Typically, a consumer of the class only needs to be aware of all the public fields.
	* Imagine needing to know / manipulate buffers in iostream in order to print "Hello World"!

## Scope Resolution Operator (::)
* When a member function is defined, the definition must include the class name because there may be two or more classes that have member functions with the same name.
* Without it, the compiler does not know which class’ member function the definition is for.

## Accessor and Mutator Functions
* A function that simply returns private members’ values are called accessor (getter) functions (i.e. they access the data).
* A function that simply sets private members’ values are called mutator (setter) functions (i.e. they change the data).

## Constructors
* A special kind of function with the same class name that it’s defined in.
* A constructor is called when an object of that class is declared.
* Constructors are the only functions that do not have a return type.
* Default constructors can be defined by you (which is good style).
* If a default constructor is not defined, the compiler will generate one if no other constructor is defined! <b>Otherwise it will not.</b>

## Copy Constructor
* Take in an existing Object in a constructor's parameter and set all of its fields to the fields of the object, thus copying one object's fields to the current object.
* Copy constructors must pass its parameter by reference…
* If a copy constructor is not defined, then the compiler will generate one. However, this copy constructor only does a SHALLOW copy.
	* Think of it as copying the reference of memory, not the memory contents.
	* Two references may now share the same memory of an object…
* Try it: Comment out the defined copy constructor and note that
```
Person s;
Person t = s;
```
still works. If the copy constructor is defined, then the assignment operator `=` will call the defined copy constructor. If the copy constructor is not defined, the default copy constructor is used.

### Shallow Copy illustration

```
// modify class Person.h definition with vector v
#include <vector>
public:
	std::vector<int>* getVector() const;

private:
	std::vector<int>* v;
```

```
// modify constructor in Person.cpp to initialize vector and push 100 into it
Person::Person() {
	name = "default name";
	age = 0;
	v = new vector<int>();
	v->push_back(100);
}

// Accessor function for the vector v
vector<int>* Person::getVector() const {
	return v;
}
```
```
// main.cpp

// function to print out contents of the vector
void printVector(vector<int> v) {
	for (int i = 0; i < v.size(); i++) {
		cout << v[i] << endl;
	}
}

// in main()
s.getVector()->push_back(200);
printVector(*s.getVector()); // 100 200
printVector(*t.getVector()); // 100 200
```

* Vector is shared between two objects due to the shallow copy!
* One way to do a "deep copy" of the vector is

```
Person::Person(Person& person) {
	name = person.getName();
	age = person.getAge();
	v = new vector<int>();
	
	// DEEP COPY
	for (int i = 0; i < person.getVector()->size(); i++) {
		v->push_back(person.getVector()->at(i));
	}
	cout << "copy constructor" << endl;
}
```

## Example of Overloading the Assignment Operator

```
// Person.h
public:
	Person& operator=(const Person& rhs);
```

```
// Person.cpp
Person& Person::operator=(const Person& rhs) {
	cout << "overloaded assignment operator" << endl;
	
	// check self-assignment, p1 = p1
	if (this == &rhs) {
		return *this;
	}
	this->name = rhs.name;
	this->age = rhs.age;
	this->v->clear();

	for (int i = 0; i < rhs.v->size(); i++) {
		v->push_back(rhs.v->at(i));
	}
	return *this;
}
```

## Copy Constructor vs. Assignment Operator

* The copy constructor is invoked when the object does not exist yet and you’re trying to assign an existing object to a new object.
* Example:

```
int main() {
	Person s;
	cout << "&s = " << &s << endl;
	Person t = s; // copy constructor
	cout << "&t = " << &t << endl;
	cout << "---" << endl;
	Person a;
	Person b;
	a = b;	// overloaded assignment operator
}
```

## Destructor
* A special member function that is called when a reference to an object
	* Goes out of scope.
	* Or a pointer to the object is called with <b>delete</b>.
* Example

```
// Person.h
public:
	~Person(); 	// destructor
```

```
// Person.cpp
Person::~Person() {
 	delete v; // delete vector that should exist on the heap.
 	cout << "DELETED: v" << endl;
}
```

## Example illustrating destructor call when exiting function

```
// main.cpp
#include <iostream>
#include "Person.h"

using namespace std;

void f() {
	Person* p = new Person(); // default constructor assigns object on the heap
	delete p; 	// manually call default constructor
				// Memory leak in the heap if call is not made.

	// Person p2; // default constructor on the stack
	// when function exits, invokes destructor for objects on the stack.
}

int main() {
	f();
	cout << "exiting main..." << endl;
	return 0;
}
```

## Big Three (Rule of Three)

* Rule of thumb: If you are implementing your own version of a copy constructor, destructor, or assignment operator, then you should implement all three.
* Important when manually managing memory on the heap.
* A good link illustrating the Big Three ... in the context of programming a video game :)
	* https://www.youtube.com/watch?v=F-7Rpt2D-zo
