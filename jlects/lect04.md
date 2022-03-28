---
num: "lect04"
lecture_date: 2021-01-13
desc: "Pointer arithmetic with Array structures. Dynamic Memory"
ready: true
annotatedready: false
---
## Relevant topics in the textbook:
Data Structures and Other Objects Using C++ Chapter 4.1

# Pointer Arithmetic

* We’ve talked about array variables referring to the memory address of the first element in the array.
* We can think of an array variable as a pointer!
* We’ve seen an example where we can either pass in an array variable OR pass in a pointer when using arrays.
* We also know that arrays must be declared with a size
* And the size must be kept track of in order to stay within the memory bounds of the memory (avoid seg faults!).

```
// Recall
// void printArray(int* values, int size) { // can use a pointer
void printArray(int values[], int size) {
	// Note: size is passed in since we won’t know how to get the size with
	// just the array variable.

	cout << values << endl; // prints memory location of start of values[]

	for (int i = 0; i < size; i++) {
		cout << "values[" << i << "] = " << values[i] << endl;
		cout << "&values[" << i << "] = " << &values[i] << endl;
		// Note: The address values are 4 bytes away since int is 4 bytes
	}
}

int main() {
	int values[3] = { 5, 10, 15 };
	printArray(values, 3);
	return 0;
}
```

* We also know that we index arrays from [0, size – 1].
* There is reason behind this!
* Under-the-hood, C++ is using the index to perform pointer arithmetic!
* When performing arithmetic to a pointer, it modifies the address by incrementing the number of bytes of the pointer’s type size.

## Example

```
int main() {
	int arr[5] = {0,1,2,3,4};
	int* x = arr;

	cout << arr << endl;
	cout << x << endl;

	cout << x + 1 << endl; // address is incremented by 1*sizeof(int)
	cout << x + 2 << endl; // address is incremented by 2*sizeof(int)
	cout << x + 3 << endl; // address is incremented by 3*sizeof(int)

	cout << *(x + 2) << endl;	// equivalent to x[2] or arr[2]
	cout << &(*(x + 2)) << endl;  // equivalent to x + 2
	return 0;
}
```

## Illustration

* The array index is the "offset" from the start of the array
* To access specific elements in the array using pointer arithmetic, the address is calculated as:

```
elementAddress = startOfArrayAddress + (i * (size of type pointer is pointing to))
```


## Example - trace the code

```
int arr[] = {10,15,20};
int* x;
x = arr;
cout << x + 1 << endl; // Address of arr[1]
cout << *x + 1 << endl; // 11
```

* x + 1 uses pointer arithmetic to calculate a memory address
* *x + 1 defeferences the array pointer and adds 1 to the first element

## Example - using [ ] and pointer arithmetic

* Assume we have a function that initializes an array:

```
void initializeArray(int* values, int size, int initialValue) {
	for (int i = 0; i < size; i++) {
		values[i] = initialValue;
		cout << values[i] << “ “;
	}
}
```

* We can also write this same algorithm using pointer arithmetic:

```
	for (int i = 0; i < size; i++) {
		*(values + i) = initialValue;
		cout << *(values + i) << " ";
	}
```

## Segmentation Faults

* If you're trying to access memory outside the range of an array, you may be accessing junk data or your program may crash with a <b>segmentation fault</b>

```
for (int i = 0; i < 1000000; i++) {
	*(values + i) = initialValue;
}
```

## Another Example - passing pointers by value / reference

```
void incrementPointer(int* p) {
	p++;
}

int main() {
	int arr[] = {10,20,30};
	int* x = arr;

	incrementPointer(x);

	cout << *x << endl; // 10
	return 0;
}
```

* Remember that even though pointers contain memory addresses, the pointer variable is a variable with its own address.
* The scenario above passes the pointer by value.
* Any modification we make to the pointer’s address in incrementPointer is local to the incrementPointer function.


* What can we do to actually increment the array using the incrementPointer function?

* We can pass the pointer by reference.

```
void incrementPointer(int*& p) {
	p++;
}
```


* We can pass a pointer to a pointer.

```
void incrementPointer(int** p) {
	//p++;		
	*p = *p + 1;	// need to modify the original pointer’s address
}

int main() {
	int arr[] = {1,2,3};
	int* x = arr;

	incrementPointer(&x); 	// since a pointer to a pointer expects the address of
				// a pointer to an int. 
	cout << *x << endl;
	return 0;
}
```


# Dynamic Memory Management

* So far, we have been working exclusively with static allocation and stack memory.
* ... but there are situations where knowing the exact size BEFORE runtime is limiting.
* It’s not feasible to store dynamically growing / shrinking objects on the stack!
* For dynamically allocating memory during the execution of a program, there’s the free store, or more commonly known as the heap.

# Heap
* The heap allows users to manually decide when, how much, and what will be stored in it.
* On the flip side, you must also decide when memory will be deallocated (deleted) in order to reuse it.
* <b>Q:</b> What happens if you forget to delete stuff from the heap?
	* Memory leaks! Memory space is finite and eventually your program will crash if unused memory is not being deleted.
* <b>Q:</b> But we can store strings of different sizes on the stack... what’s up with that?
	* On the stack, strings are a fixed size containing fields such as the length of the string, and a memory address to the sequence of characters on the heap.
	* Note that a memory address and integer size ARE of fixed length (as well as other information the string class may have).
	* Behind the scenes, as strings may grow and shrink on the heap, the address that points to the sequence of chars on the heap can change.
* The programmer manages heap memory space manually.

## "new" operator

* The primary use for pointers are to access objects that have been dynamically allocated on the heap.
* The result of "new" is a pointer to the object that was allocated on the heap.

## Example
```
int* p = new int(10);	// allocate an int on the heap and point p to it
*p = 2;			// sets the int value to 2 (without address change)
int& q = *p;		// q refers to the value that p points to
q = 4;			// change int value to 4

cout << *p << endl;	// prints 4

int* r = &q;		// make r point to the address that q refers to
*r = 6;			// change int value that r points to to 6

cout << *p << endl;	// prints 6
cout << q << endl;	// prints 6
cout << *r << endl;	// prints 6
```


## "delete" operator

* Anytime you use the “new” operator, consider if you need to eventually delete the memory it consumes.
	* Otherwise, your program will have memory leaks and eventually crash!

## Example of memory leaks

```
void g(int x) {
	int* p = new int(x);	// memory leak!
	delete p;		// remove this and see application size grow!
	return;
}

int main() {
for (int i = 0; i < 100000000; i++)
		g(i);
}
```

* Check size of the memory being used for the process with:
'''
ps -o pid,user,%mem,command ax | sort -b -k3 -r
'''

* since int* p in g() is a local variable, this gets removed from the stack, BUT THE VALUE ON THE HEAP REMAINS.
	* Once the variable is removed when the function exits, there is no way to remove this from the heap.
		* This is a memory leak!
* "delete" is the opposite of new
	* "new" creates an object on the heap and returns a pointer to it.
	* "delete" takes a pointer and removes the data from the heap.
		* "delete p;" doesn’t delete the variable p, it deletes what p points to on the heap!
		* "delete" only works for values that exist on the heap.

# Dangling Pointers
* After a pointer’s memory is deleted, the pointer itself is still available to use.
* BUT, you should never use a dangling pointer (the behavior of it is undefined).
	* And why would you want to use a pointer to something that shouldn’t be there?

## Dangling Pointers Example

```
int g(int x) {
	double* p = new double(x);
	delete p;	// delete value from the heap
	return *p; 	// p is a dangling pointer since heap contents were removed!
			// Results in undefined behavior. Shouldn’t do this!
}
```

# Dynamically allocating arrays
* We have been allocating arrays on the stack, but we can also do this on the heap!
	* Actually, we SHOULD do this on the heap if our array size is not known during compile time.
	* Example of declaring and deleting an array on the heap. 

```
int* arr = new int[10];	// create an array of 10 integers on the heap
delete [] arr;		// removes the array from the heap. Note the [] syntax for deleting arrays from the heap.
```

* Some compilers may have extended functionality to support dynamically allocating arrays using the syntax for statically allocating arrays.
	* For example, g++/clang++ allows this, but VisualStudio currently does not:

```
int x;
cout << "Enter a positive number: ";
cin >> x;
// int intArray[x]; // ERROR IN VisualStudio, NOT g++ / clang++
int* intArray = new int[x]; // LEGAL IN BOTH
for (int i = 0; i < x; i++) {
	intArray[i] = i;
	cout << intArray[i] << endl;
}

// Note: to delete an array on the heap, use delete [] intArray;
delete [] intArray;
```
