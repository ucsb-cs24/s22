---
num: "lect11"
lecture_date: 2021-02-17
desc: "Vectors, Queues, Stacks, iterators."
ready: true
annotatedready: false
---
## Relevant topics in the textbook:
Data Structures and Other Objects Using C++ Chapters 5.6, 7, 8


# Standard Libarary Containers
There are many implementations of containers.
* Containers are data abstractions where you can store a sequence of elements.
… and iterators...
* Iterators are a common part of these containers, which allow you to "iterate" through the components
* Depending on the container, you can even read / write from / to these elements

## std::Vector
* A vector is a sequence of objects that are conceptually stored one after the other
* Vectors are implemented with templates, so you can store one kind of object type in the vector container


```
// main.cpp
#include<vector>

using namespace std;

int main() {
	vector<int> v; // a vector containing int elements
return 0;
}
```
Under-the-hood, vectors are implemented using arrays and behave similar to arrays.
* Vectors can be indexed starting from 0 to size – 1
Yet they’re different than arrays…
* Vectors are dynamically-resizable
* Vectors have a size associated with it.
	*Arrays do not know their size and the programmer must be aware of it.

## Adding to a vector example
```
// main.cpp
#include<iostream>
#include<vector>

using namespace std;

template <class T>
void printVector(vector<T> &v) {
	for (int i = 0; i < v.size(); i++) {
		cout << "v[" << i << "] = " << v[i] << endl;
	}
}

int main() {
	vector<int> v;
	for (int i = 0; i < 5; i++) // it could be any reasonable size…
		v.push_back(i);

	printVector(v);
	return 0;
}
```
* Like arrays, if you index a vector element that is out of range, you will probably get junk data or make your program crash.
* You can also use the .at() function to access an element.
* Unlike [ ], if .at() references an element that the vector doesn’t contain, an exception is thrown (more on exceptions later).

## Example
```
cout << v.at(4) << endl;
cout << v.at(5) << endl; // EXCEPTION THROWN
cout << v[5] << endl; // JUNK
```

Other supported operations are:
* front() – returns the first element
* back() – returns the last element
* pop_back() – delete the last element

```
cout << "v.front() = " << v.front() << endl;
cout << "v.back() = " << v.back() << endl;
v.pop_back();
printVector(v);
```

## Vector Initialization
`push_back()` is one way to create elements in a vector. Though it’s not the only way
* You can declare a vector with a size initially
* You can also initialize a vector with a size and default values.

## Example:
```
vector<int> v1(100); // initializes vector with 100 elements.
vector<int> v2(100, 1); //initializes vector with 100 elements = 1
```

## Example creating a vector on the heap with a pointer reference to the vector contents on the heap
```
vector<int>* v = new vector<int>(10,1); // vector on heap with 10 elements initialized to 1
cout << v->size() << endl; // 10
cout << sizeof(v) << endl; // 8 bytes since v is a pointer
printVector(*v);

vector<int> w;
cout << sizeof(w) << endl; // 24 since w is a vector object
```

* A vector maintains the state of a dynamic array on the heap (which is why we do not need to specify a size when initializing a vector like we do with an array).
* Regardless of the contents of the array, the size of the vector w on the stack will always be constant.
    * The vector class has fields such as a pointer to an array on the heap, values to keep track of the size and capacity, etc.
    * Therefore, all vectors constructed on the stack will have the same memory footprint on the stack.

# Iterators
* An iterator is an abstraction for a position in a collection of objects.
* Container classes in the C++ standard library support iterators.
* It’s common to think of an iterator as a pointer to an element’s position
* Though technically it’s not a pointer, but most likely uses a pointer in its implementation.
* Even though iterators are supported between different types of containers, an iterator can only be used with its own container type.

## Example
```
vector<string> v2;

v2.push_back("Hello.");
v2.push_back("My");
v2.push_back("name");
v2.push_back("is");
v2.push_back("Batman");

for (vector<string>::iterator i = v2.begin(); i < v2.end(); i++) {
	cout << *i << " "; // string value
	cout << i->size() << endl; // prints the size of the strings
}
```
In the above example, we’ve seen vector functions that deal specifically with iterators.
* begin() – returns an iterator that points to the first element
* end() – returns an iterator that points just past the last element
* ++ increments the iterator to the next element
* < compares positions of the iterator
* `*` dereferences an iterator to get the object

## Example (Showing different ways to index elements using iterators):
```
vector<string>::iterator i = v2.begin();
cout << v2[4] << endl; 		// Batman
cout << i[4] << endl;		// Batman
cout << *(i + 4) << endl;	// Batman
```

In order to erase items in the vector, there is an `erase` method that requires iterators to do this

## Example of erasing elements
```
// Removing 2nd index of the vector
// v2.erase(v2.begin() + 2); // remove "name"
// printVector(v2);

// Removing 1st and 2nd index - [1,3)
v2.erase(v2.begin() + 1, v2.begin() + 3);
printVector(v2);
```

# Stack
```
#include<iostream>
#include<stack>

using namespace std; 
  
void printStack(stack<int> s) 
{ 
    while (!s.empty()) 
    { 
        cout << s.top() << endl; 
        s.pop(); 
    } 
} 
  
int main () 
{ 
    stack <int> s; 
    s.push(1); 
    s.push(2); 
    s.push(3); 
    s.push(4); 
    s.push(5); 
  
    cout << "Current content of stack: " << endl; 
    printStack(s); 
  
    cout << "Size of stack: " << s.size() << endl; 
    cout << "Top of the stack " << s.top() << endl; 
  
    s.pop(); 
    
    cout << "Current content of stack:" << endl; 
    printStack(s); 
  
    return 0; 
} 
```

#Queue
```
#include<iostream>
#include<queue>

using namespace std; 
  
void printQueue(queue<int> q) 
{ 
    while (!q.empty()) 
    { 
        cout << q.front() << endl; 
        q.pop(); 
    } 
} 
  
int main () 
{ 
    queue <int> q; 
    q.push(1); 
    q.push(2); 
    q.push(3); 
    q.push(4); 
    q.push(5); 
  
    cout << "Current content of queue: " << endl; 
    printQueue(q); 
  
    cout << "Size of queue: " << q.size() << endl; 
    cout << "Front of the queue " << q.front() << endl; 
    cout << "Back of the queue " << q.back() << endl;
  
    q.pop(); 
    
    cout << "Current content of queue:" << endl; 
    printQueue(q); 
  
    return 0; 
} 
```

