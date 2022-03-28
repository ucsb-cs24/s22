---
num: "lect03"
lecture_date: 2021-01-11
desc: "Where does memory go? Stack and Heap"
ready: true
annotatedready: false
---
## Relevant topics in the textbook:
Data Structures and Other Objects Using C++ Chapter 4.1

# Structs - refreshment

* Structs are a programmer-defined type containing a set of associated values with possibly varying types.
* C++ gives us a lot of tools and types to work with out-of-the-box.
	* However, it’s impossible for a programming language to give us all possible types of abstractions
	* Programmers can organize data into types that fit the needs of an application.

## Defining a struct

```
struct Student { // Student is now a new defined type
	string name;
	int perm;
	double tuition;
}; // Syntactically, a ‘;’ is needed at the end of a struct definition.
```

* You can use the ‘.’ operator to assign values to and access values from a member of a struct type.

## Example

```
int main() {
	Student s1; // defining a variable containing the struct type Student
	s1.name = "Chris Gaucho";
	s1.perm = 1234567;
	s1.tuition = 3000.50;

	cout << "Name: " << s1.name << ", perm: " << s1.perm
		 << ", tuition: " << s1.tuition << endl;

	return 0;
}
```

* We can use this representation to do more interesting things like keep collections of students in a class, department, university, etc.

## Struct values as pointers

* A pointer can point to any C++ type, including structs!

```
Student* s2 = &s1; // OK
s2.name = "Mr. E"; // ERROR! Why?
```

* The code above won’t work because s2 is a pointer containing an address to a Student struct.
	* Remember, pointers contain memory addresses to a type!
	* If we wanted to modify a memory address, we would have to dereference the pointer.

```
*s2.name = "Mr. E"; // Still contains an error!
```

* In this case, the ‘.’ operator has precedence over the ‘*’ operator.
	* So it’s still trying to access the name field from a pointer variable without dereferencing it.
* One way to correct this is to dereference the variable first, then access the struct’s variable.

```
(*s2).name = "Mr. E"; // OK. Pointer is dereferenced first, then name is accessed
```

* When dealing with pointers, this mechanism is so common that there is a shortcut to do this.
* The ‘->’ operator is used.

```
s2->name = "Mr. E"; // OK. Same as (*s2).name
```

# Reference Variables

* Reference variables are considered another alias to a variable that was assigned to it.
	* Any changes to either variable are reflected in both variables.

```
int x = 100;
int& y = x; // y references x

cout << x << ", " << y << endl;
x = 500;
cout << x << ", " << y << endl;
x = 200;
cout << x << ", " << y << endl;
```

## Some differences between reference variables and pointers

* Reference variables may not change after it was assigned to reference another variable.
	* Pointers can change what it’s pointing to.
* Reference variables must be initialized.
	* Pointers can be uninitialized.
* Reference variables cannot refer to other reference variables
	* Pointers can have pointers to pointers to pointers …
* Reference variables’ address is the same address as the variable it binds to.
	* Pointers’ values have the address it points to, but occupies its own space on the stack and has its own memory address.
	* So when we pass-by-reference, we are technically using reference variables that are using the same memory address as the function caller’s parameter variables.

## Example (observe the addresses)

```
int a = 10;
int* p = &a;
int& r = a;

cout << "a = " << a << endl;
cout << "&a = " << &a << endl;
cout << "p = " << p << endl;
cout << "&p = " << &p << endl;
cout << "r = " << r << endl;
cout << "&r = " << &r << endl;
```

# Memory Stack

* Types are important in compiled languages like C++
	* Knowing exactly the amount of memory a function will occupy is essential for memory organization during execution.
	* Function calls are laid out in memory as a data structure called a <b>stack</b>.
		* Think of a stack like a canister of tennis balls.
		* You can only add to the top of the stack.
		* You can only remove an item at the top of the stack.
	* Every time a function is called, memory footprint is created and added to the top of the memory stack.
	* When the function returns a value, the memory reserved for the function is removed from the stack.
	* `int main()` is the bottom most function on the stack throughout execution.

## Example

```
#include <iostream>

using namespace std;

int doubleValue(int x) {
	return 2 * x;
}

int quadrupleValue(int x) {
	return doubleValue(x) + doubleValue(x); 
}

int main() {
	int result = quadrupleValue(4);
	cout << result << endl;
	return 0;
}
```

* Start Execution

```
|                       |
|-----------------------|
| int main()            |
|_______________________|
```

* `quadrupleValue(4)` is called

```
|                       |
|-----------------------|
| int quadrupleValue(4) |
|-----------------------|
| int main()            |
|_______________________|
```

* `doubleValue(x)` is called

```
|                       |
|-----------------------|
| int doubleValue(4)    |
|-----------------------|
| int quadrupleValue(4) |
|-----------------------|
| int main()            |
|_______________________|
```

* `doubleValue(4)` finishes executing and returns a value

```
|                       |
|-----------------------|
| int quadrupleValue(4) |
|-----------------------|
| int main()            |
|_______________________|
```

* `doubleValue(4)` is called again

```
|                       |
|-----------------------|
| int doubleValue(4)    |
|-----------------------|
| int quadrupleValue(4) |
|-----------------------|
| int main()            |
|_______________________|
```

* `doubleValue(4)` finishes executing and returns a value

```
|                       |
|-----------------------|
| int quadrupleValue(4) |
|-----------------------|
| int main()            |
|_______________________|
```

* `quadrupleValue` returns the sum of the two `doubleValue(4)` function calls

```
|                       |
|-----------------------|
| int main()            |
|_______________________|
```

* `main` prints the result of `quadrupleValue` return value. Program exits.


# Stack vs heap:
* memory management (stack - automatic, heap - manual)
* available memory size (larger in heap)
* memory fragmentation (heap) vs continuous allocation (stack)
* fixed memory allocation (stack) vs flexible - resizing (heap)
* memory time access (slower for heap)
