---
num: "lect14"
lecture_date: 2021-03-01
desc: "Binary Search Trees"
ready: true
annotatedready: false
---
## Relevant topics in the textbook:
Data Structures and Other Objects Using C++ Chapter 10

# Trees

* A collection of connected nodes
* One of the nodes is the "Root node"
* Each node can have many children nodes, but only a single parent node.

## Important terms:

* Root node
* Leaf node
* Subtree
* Parent node
* Key
* Level
* Degree

# Binary Trees

* Each node can have at most two children nodes


# Binary Search Trees

* The left subtree of a node contains only nodes with keys lesser than the node's key
* The right subtree of a node contains only nodes with keys greater than the node's key
* No duplicate nodes

Good visualizations can be found [here](https://visualgo.net/bn/bst) and [here](https://www.cs.usfca.edu/~galles/visualization/BST.html)

# Code:

//Makefile
```
CXX=g++

main: main.o bst.o
	${CXX} -o main -std=c++11 main.o bst.o

clean:
	rm -f *.o main
```

//Main.cpp
```
#include <iostream>
#include "bst.h"

using namespace std;


int main() {
	int a[] = {0,1,2,3,4,5,6,7,8,9};
	int b[] = {9,8,7,6,5,4,3,2,1,0};
	int c[] = {0,9,1,8,2,7,3,6,4,5};
	int d[] = {5,4,6,3,7,2,8,1,9,0};
	int e[] = {5,2,7,3,8,4,6,1,9,0};

	BST tree;

	for(int i=0; i<10; i++){
		cout << endl;
		tree.root = tree.insert(a[i], tree.root);
	}

	cout << tree.root->key << endl;
	cout << tree.root->right->key << endl;
	//cout << tree.root->right->left->key << endl;


	Node* node = tree.search(11, tree.root);
	if (node == NULL){
		cout << "Value not found." << endl;
	}
	else {
		cout << node->key << endl;
	}
	
}
```

//bst.h
```
class Node{
	public:
		Node(int key);
		int key;
		Node* right;
		Node* left;
};

class BST{
	public:
		BST();
		Node* root;
		Node* insert(int key, Node* node);
		Node* search(int key, Node* node);
};
```

//bst.cpp
```
#include<iostream>
#include "bst.h"

using namespace std;

Node::Node(int key){
	this->key = key;
	this->right = NULL;
	this->left = NULL;
	cout << "Node constructor: " << key << endl; 
}


BST::BST(){
	this->root = NULL;
}

Node* BST::insert(int key, Node* node){
	if (node == NULL){
		cout << "Node does not exist. Creating one" << endl;
		node = new Node(key);
	}
	else if (key > node->key){
		cout << "Value greater than current data. Go right." << endl;
		node->right = insert(key, node->right);
	}
	else if (key < node->key){
		cout << "Value smaller than current data. Go left." << endl;
		node->left = insert(key, node->left);
	}
	
	return node;

}

Node* BST::search(int key, Node* node){
	if (node == NULL or node->key == key){
		return node;
	}
	if (key > node->key){
		search(key, node->right);
	}
	else if (key < node->key){
		search(key, node->left);
	}

}

```
