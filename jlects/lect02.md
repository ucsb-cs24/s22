---
num: "lect02"
lecture_date: 2021-01-06
desc: "Introduction to pointers. Pass-by-value, pass-by-reference"
ready: true
annotatedready: false
---
## Relevant topics in the textbook:
Data Structures and Other Objects Using C++ Chapter 4.1

# Memory Addresses

* We can find out what the memory address of variables stored in memory using the ‘&’ symbol.

```
int i = 1;
cout << &i << endl;
```

* Memory addresses are usually byte-addressable and displayed in hexadecimal notation.

# Pointers

* Pointers contain the memory address of a variable.
* Pointers are two things:
	* A memory address
	* A type
* Therefore a pointer represents <i>a memory location storing a specific type</i>.
* Size of a pointer depends on the operating system the application is running on.
	* 64-bit Operating Systems can map to 2<sup>64</sup> memory addresses.
	* 32-bit Operating Systems can map to 2<sup>32</sup> memory addresses

## Example of declaring a pointer

```
int* p; // p is a pointer to an int type
cout << sizeof(p) << endl; // pointer address is 8 bytes since I have a 64-bit OS
cout << p << endl;
```

* Note: p is not an `int` type. It should contain a memory address where an int is located.

```
int i = 1;
//int* p = i; 		// can’t do this! i is an int, not a pointer to an int
int* p = &i; 		// OK. p points to the address of i
cout << p << endl;
int* q = p; 		// make q point to the same place p does (& not needed)
cout << q << endl;
```

## Dereferencing Pointers

* When you want to access a value of an object that a pointer points to, you must use the dereferencing operator (*).
* Or we can overwrite the memory location a pointer is referring to by assigning a value to a dereferenced pointer.

## Larger example with dereferencing pointers

```
int i = 1;
int* p = &i; // point to memory location of int i var

cout << "p points to the memory address " << p << endl;
cout << "p points to the integer value " << *p << endl;
cout << "----" << endl;

*p = 10; // change value in the memory address.

cout << "p points to memory address " << p << endl;
cout << "p points to the integer " << *p << endl;
cout << "i = " << i << endl;
cout << "----" << endl;

i = 25;

cout << "p points to memory address " << p << endl;
cout << "p points to the integer " << *p << endl;
cout << "i = " << i << endl;

p = NULL; // or assign p = 0;
cout << p << endl;
cout << *p << endl;
```

## Example of pointers to pointers

* Possible to chain pointers by having pointers point to pointers that point to pointers ...
* For the example below, follow along and observe the memory addresses:

```
// A larger example (with pointers to pointers)
int x = 5, y = 10, z = 15;
int* p1 = &x;
int* p2 = &y;

p2 = p1;
int** p3; // pointer pointing to another pointer
p3 = &p1;
p1 = &z;

x /= 5;
y /= 5;
z /= 5;

cout << "x = " << x << endl;
cout << "&x = " << &x << endl;
cout << "y = " << y << endl;
cout << "&y = " << &y << endl;
cout << "z = " << z << endl;
cout << "&z = " << &z << endl;
cout << "----" << endl;

cout << "&p1 = " << &p1 << endl;
cout << "p1 = " << p1 << endl;
cout << "*p1 = " << *p1 << endl;
cout << "----" << endl;

cout << "&p2 = " << &p2 << endl;
cout << "p2 = " << p2 << endl;
cout << "*p2 = " << *p2 << endl;
cout << "----" << endl;

cout << "&p3 = " << &p3 << endl;
cout << "p3 = " << p3 << endl;
cout << "*p3 = " << *p3 << endl;
cout << "**p3 = " << **p3 << endl;
```

# Pass-by-reference vs. pass-by-value

* Also known as call-by-value and call-by-reference.
* Pass-by-value copies the parameter value into a variable that is local to the function.
* Pass-by-reference modifies the value in memory and does not create a local copy.

* Example of pass by value

```
// pass by value
void addTwo(int x) {
	x = x + 2;
	cout << x << endl;
}

int main() {
	int a = 10;
	cout << "a = " << a << endl; // 10
	addTwo(a);
	cout << "a = " << a << endl; // 10
}
```

* Example of pass by reference

```
// pass by reference
void addTwo(int &x) {
	x = x + 2;
	cout << x << endl;
}

int main() {
	int a = 10;
	cout << "a = " << a << endl; // 10
	addTwo(a);
	cout << "a = " << a << endl; // 12 – changes value in memory location
}
```

* Pass by reference can be thought of using the value's memory address.
	* Any changes in the function will reflect the value outside of the function.
	* Pass by reference can be more efficient – if a copy of a very large type is passed in, can be inefficient.
	* Can be useful if we want the function to change a value globally.
* Pass by value may be useful if you want to keep the original value unmodified after a function uses it.

* You can also pass pointers into functions.

```
void addTwo(int* x) {
	*x = *x + 2;
	cout << *x << endl;
}

int main() {
	int a = 10;
	cout << "a = " << a << endl;
	addTwo(&a); // pointers are memory addresses, need to pass this.
	cout << "a = " << a << endl;
}
```

* Since we're modifying the memory location referred to by a pointer, this behaves similar to pass-by-reference.

## Passing arrays into functions

```
void printArray(int values[], int size) {
	// Note: size is passed in since we won’t know how to get the size with
	// just the array variable.

	cout << values << endl; // prints memory location of start of values[]

	for (int i = 0; i < size; i++) {
		cout << "values[" << i << "] = " << values[i] << endl;
		cout << "&values[" << i << "] = " << &values[i] << endl;
		// Note: The address values are 4 bytes away since an int type is 4 bytes
	}
}

int main() {
	int values[3] = { 5, 10, 15 };
	printArray(values, 3);
	return 0;
}
```

* Under-the-hood, arrays are pointers referring to the memory location of the first element in the array.
* We can redefine the printArray signature with a pointer value and this will still work:

```
void printArray(int* values, int size)
```





