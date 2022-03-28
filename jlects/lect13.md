---
num: "lect13"
lecture_date: 2021-02-24
desc: "Quicksort. Prefix, Postfix and Infix notation"
ready: true
annotatedready: false
---
## Relevant topics in the textbook:
Data Structures and Other Objects Using C++ Chapter 13.2

# Notation:

## Infix
* Expression: X + Y
* Expression: A * B + C / D
* Expression: A * (B + C / D)

## Prefix ("Polish notation")
* Expression: + X Y
* Expression: + * A B / C D
* Expression: * A + B / C D

## Postfix ("Reverse Polish notation")
* Expression: X Y +
* Expression: A B * C D / +
* Expression: A B C D / + *

# Divide and conquer
* Subdivide a larger problem into smaller parts
* Solve each smaller part
* Combine solutions of smaller sub problems back into the larger problem
* We see this pattern in recursive problems where they can be subdivided

# Divide and conquer sorting algorithms
* You’ve learned about quadratic sorting algorithms
	* Bubble sort, selection sort, insertion sort
		* Runs in O(n<sup>2</sup>)
	* Better sorting algorithms exist
		* Can improve our run time to O(nlogn) in the worst case.

# Mergesort
* Idea:
	* Break an array into sub arrays where size = 1.
	* Merge each small sub array together to form sorted larger array.
	* Apply technique to the entire array.
	* Sorting is done “bottom-up”

* Good visualization is given [here](https://opendsa-server.cs.vt.edu/embed/mergesortAV) and [here](https://visualgo.net/bn/sorting)

# Mergesort Analysis

* Best-case: O(nlogn)
* Average-case: O(nlogn)
* Worst-case: O(nlogn)
* Requires O(n) additional space to merge the unsorted arrays into a sorted array
	* Time / space tradeoff

# Quicksort
* Idea:
	* Can subdivide array based on a “pivot” value.
		* Place elements < pivot to the left-side of the array
	* Place elements > pivot to the right-side of the array
		* Repeat for each left / right portion of the array
	* When sub array sizes = 1, then entire array is sorted
	* Sorting is done “top-down”

* Good visualization is [here](https://opendsa-server.cs.vt.edu/embed/quicksortAV)


# Quicksort Algorithm

```
// Makefile
add quicksort.o to dependencies
```

```
// quicksort.h

class Quicksort{
	public:
		void printArray(const int a[], size_t size);
		void partition(int a[], size_t size, size_t& pivotIndex);
		void sort(int a[], size_t size);
};
```

```
// quicksort.cpp

#include<iostream>
#include "quicksort.h"

using namespace std;

void Quicksort::printArray(const int a[], size_t size) {
	cout << "Printing Array" << endl;
	for (int i = 0; i < size; i++) {
		cout << "a[" << i << "] = " << a[i] << endl;
	}
}

void Quicksort::partition(int a[], size_t size, size_t& pivotIndex) {
	int pivot = a[0];		 // choose 1st value for pivot
	size_t left = 1;		 // index just right of pivot
	size_t right = size - 1; // last item in array
	int temp;
	cout << endl <<"Chose a pivot: " << pivot << endl;
	printArray(a, size);
	while (left <= right) {
		// increment left if <= pivot
		while (left < size && a[left] <= pivot) {
			left++;
		}

		// decrement right if > pivot
		while (a[right] > pivot) {
			right--;
		}

		// swap left and right if left < right
		if (left < right) {
			cout << "Swapping: " << a[left] << " with " << a[right] << endl;
			temp = a[left];
			a[left] = a[right];
			a[right] = temp;
			printArray(a, size);
		}
	}
	cout << "Swapping pivot: " << a[0] << " with " << a[right] << endl;
	// swap pivot with a[right]
	pivotIndex = right;
	temp = a[0];
	a[0] = a[pivotIndex];
	a[pivotIndex] = temp;
	printArray(a, size);
}

void Quicksort::sort(int a[], size_t size) {
	size_t pivotIndex;		// index of pivot
	size_t leftSize;		// num elements left of pivot
	size_t rightSize;		// num elements right of pivot
	
	

	if (size > 1) {
		// partition a[] based on pivotIndex
		partition(a, size, pivotIndex);

		// Compute the sizes of left and right sub arrays
		leftSize = pivotIndex;
		rightSize = size - leftSize - 1;

		// recursive call sorting the left array
		sort(a, leftSize);

		// recursive call sorting the right array
		sort((a + pivotIndex + 1), rightSize);
	}
}
```

```
// add to main.cpp
#include "quicksort.h"
```

# Quicksort Analysis

* Best-case: O(nlogn)
* Average-case: O(nlogn)
* Worst-case: O(n<sup>2</sup>)
	* Quicksort performs poorly depending on the pivot value chosen.
		* Run this algorithm with an array already in sorted order.
	* If the pivot is the least or greatest value in the array, then the sub arrays aren't evenly divided.
	* An optimization to try and prevent this scenario is to select a few pivot values in the array randomly and selecting the medium of these.
* Unlike (our version of) Mergesort, Quicksort does not require additional buffer space and can sort the array in-place.
