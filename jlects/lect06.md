---
num: "lect06"
lecture_date: 2021-01-25
desc: "Template functions"
ready: true
annotatedready: false
---
## Relevant topics in the textbook:
Data Structures and Other Objects Using C++ Chapter 6.1

# Template functions

* Code examples

* Comparison of different types:

```
#include <iostream>

using namespace std;


template<class T>
T maxValue(T x, V y){
	if (x > y) {return x;}
	else {return y;}
}


int main() {
	cout << maxValue(1, 2) << endl;
	cout << maxValue(1.3, 1.5) << endl;
	cout << maxValue('a', 'b') << endl;

	return 0;
}
```

* Using arrays and helper functions:

```
#include <iostream>

using namespace std;

void printArray(int *arr, size_t s){
	cout << arr << endl;
	for(int i=0; i < s; i++){
		cout << "Array element: " << i << " is : " << arr[i] << endl;
	}
}

void fillArrayConst(int *arr, size_t s, int init_val){
	cout << arr << endl;
	for(int i=0; i < s; i++){
		arr[i] = init_val;
	}
}

void fillArrayIncr(int *arr, size_t s, int init_val){
	cout << arr << endl;
	for(int i=0; i < s; i++){
		arr[i] = init_val+i;
	}
}

int main() {

	size_t a = 10;
	char *v = new char[a];
	cout << v << endl;
	fillArrayConst(v, a, 'a');
	printArray(v, a);

	delete [] v;
	return 0;
}
```

```
#include <iostream>

using namespace std;

template<class T>
void fillArrayIncr(T *arr, size_t s, T init_val);

template<class T>
void printArray(T *arr, size_t s){
	for(int i=0; i < s; i++){
		cout << "Array element: " << i << " is : " << arr[i] << endl;
	}
}

template<class T>
void fillArrayConst(T *arr, size_t s, T init_val){
	for(int i=0; i < s; i++){
		arr[i] = init_val;
	}
}

template<class T>
void fillArrayIncr(T *arr, size_t s, T init_val){
	for(int i=0; i < s; i++){
		arr[i] = init_val+i;
	}
}

int main() {
	size_t a = 10;
	int *v = new int[a];
	cout << v << endl;
	fillArrayIncr(v, a, 1);
	printArray(v, a);

	char *w = new char[a];
	cout << w << endl;
	fillArrayIncr(w, a, 'a');
	printArray(w, a);

	delete [] v;
	delete [] w;
	return 0;
}
```
