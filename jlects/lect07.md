---
num: "lect07"
lecture_date: 2021-01-27
desc: "Operator overloading. Friend functions"
ready: true
annotatedready: false
---
## Relevant topics in the textbook:
Data Structures and Other Objects Using C++ Chapter 2.5

# Operator overloading:

* Code examples
Account.h

```
#ifndef ACCOUNT_H
#define ACCOUNT_H

#include <iostream>


class Account {
	public:
		Account(); 				
		Account(std::string name, int balance);	
		Account(Account& account);	
		Account& operator=(const Account& rhs);
		~Account();	

		Account operator+(Account& rhs);

	private:
		std::string name;
		int balance;
};



#endif
```

Account.cpp

```
#include <iostream>
#include <string>
#include "Account.h"

using namespace std;

Account::Account() {
	cout << "Default Constructor" << endl;
	name = "Checking account";
	balance = 0;
	
}

Account::Account(string name, int balance) {
	cout << "Overloaded constructor" << endl;
	this->name = name;
	this->balance = balance;
	
}

Account::Account(Account& account) {
	cout << "Copy constructor" << endl;
	this->name = account.name;
	this->balance = account.balance;
	
}

Account& Account::operator=(const Account& rhs) {
	cout << "Overloaded assignment operator" << endl;
	
	if (this == &rhs){
		return *this;	
	}

	this->name = rhs.name;
	this->balance = rhs.balance;


	return *this;
}

Account Account::operator+(Account& rhs) {
	cout << "Overloaded addition operator" << endl;

	Account a;

	// balance of b: this->balance
	// balance of c: rhs.balance
	a.balance = this->balance + rhs.balance;
	a.name = rhs.name;

	this->balance = 0;
	rhs.balance = 0;

	return a;
}


Account::~Account() {
 	cout << "Deconstructor" << endl;
}
```

main.cpp

```
#include <iostream>
#include "Account.h"

using namespace std;

int main() {
	Account a;
	Account b("Savings", 1111);
	Account c = b;
	a = b + c;
	

	cout << "exiting main..." << endl;
	return 0;
}
```

# Friend functions:

* Code examples
In Account.h add:
```
public:
	friend std::ostream &operator<<(std::ostream &output, const Account& account);
	friend std::istream &operator>>(std::istream &input, Account& account);
```

main.cpp

```
#include <iostream>
#include "Account.h"

using namespace std;

ostream &operator<<(ostream &output, const Account& account){
	output << "Account name: " << account.name << " Account balance: " << account.balance;
	return output;
}

istream &operator>>(istream &input, Account& account){
	input >> account.name >> account.balance;
	return input;
}

int main() {
	Account a;
	Account b("Savings", 1111);
	Account c = b;
	a = b + c;
	
	cout << a << endl;
	cout << b << endl;
	cout << c << endl;

	cout << "Provide new account name and new balance:" << endl;
	cin >> a;
	cout << a << endl;

	cout << "exiting main..." << endl;
	return 0;
}
```
