# C++ Programming Questions

## 1. Sum of Natural Numbers up to N

### Ans:- 

```cpp
#include <iostream>
using namespace std;
int main() {
    int n;
    cout << "Enter a positive integer n: ";
    cin >> n;
    if (n < 1 || n > 10000) {
        cout << "Please enter a number between 1 and 10,000." << endl;
        return 1;
    }
    int sum = n * (n + 1) / 2;
    cout << sum << endl;
    return 0;
}
```

## 2. Count Digits in a Number

### Ans:- 

```cpp
#include <iostream>
using namespace std;
int main() {
    int n;
    cin >> n;
    int count = 0;
    while (n > 0) {
        n /= 10;
        count++;
    }
    cout << count << endl;
    return 0;
}
```

## 3. Function Overloading for Calculating Area

### Ans:-

```cpp
#include <iostream>
using namespace std;

const double PI = 3.14159;

double areaCircle(double radius) {
    return PI * radius * radius;
}

double areaRectangle(double length, double breadth) {
    return length * breadth;
}

double areaTriangle(double base, double height) {
    return 0.5 * base * height;
}

int main() {
    double radius, length, breadth, base, height;

    cin >> radius;
    cin >> length >> breadth;
    cin >> base >> height;

    cout << areaCircle(radius) << endl;
    cout << areaRectangle(length, breadth) << endl;
    cout << areaTriangle(base, height) << endl;

    return 0;
}
```

## 4. Implement Polymorphism for Banking Transactions

### Ans:- 

```cpp
#include <iostream>
using namespace std;

class Account {
public:
    virtual void calculateInterest() = 0;
};

class SavingsAccount : public Account {
private:
    double balance;
    double rate;
    int time;

public:
    SavingsAccount(double b, double r, int t) : balance(b), rate(r), time(t) {}

    void calculateInterest() override {
        double interest = balance * (rate / 100) * time;
        cout << "Savings Account Interest: " << interest << endl;
    }
};

class CurrentAccount : public Account {
private:
    double balance;
    double maintenanceFee;

public:
    CurrentAccount(double b, double fee) : balance(b), maintenanceFee(fee) {}

    void calculateInterest() override {
        balance -= maintenanceFee;
        cout << "Balance after fee deduction: " << balance << endl;
    }
};

int main() {
    int accountType;
    double balance;

    cout << "Account Type (1 for Savings, 2 for Current): ";
    cin >> accountType;

    cout << "Balance: ";
    cin >> balance;

    if (accountType == 1) {
        double rate;
        int time;
        cout << "Interest Rate: ";
        cin >> rate;
        cout << "Time (in years): ";
        cin >> time;

        SavingsAccount savings(balance, rate, time);
        savings.calculateInterest();
    } else if (accountType == 2) {
        double maintenanceFee;
        cout << "Maintenance Fee: ";
        cin >> maintenanceFee;

        CurrentAccount current(balance, maintenanceFee);
        current.calculateInterest();
    } else {
        cout << "Invalid account type." << endl;
    }

    return 0;
}
```

## 5. Hierarchical Inheritance for Employee Management System

### Ans:-

```cpp
#include <iostream>
#include <string>
using namespace std;

class Employee {
protected:
    string name;
    int id;
    double salary;

public:
    Employee(string n, int i, double s) : name(n), id(i), salary(s) {}

    virtual double calculateEarnings() = 0;
    virtual void display() = 0;
};

class Manager : public Employee {
private:
    int rating;

public:
    Manager(string n, int i, double s, int r) : Employee(n, i, s), rating(r) {}

    double calculateEarnings() override {
        double bonus = (0.1 * salary) * rating;
        return salary + bonus;
    }

    void display() override {
        cout << "Employee: " << name << " (ID: " << id << ")" << endl;
        cout << "Role: Manager" << endl;
        cout << "Base Salary: " << salary << endl;
        cout << "Bonus: " << (0.1 * salary) * rating << endl;
        cout << "Total Earnings: " << calculateEarnings() << endl;
    }
};

class Developer : public Employee {
private:
    int extraHours;

public:
    Developer(string n, int i, double s, int hours) : Employee(n, i, s), extraHours(hours) {}

    double calculateEarnings() override {
        double overtimeCompensation = extraHours * 500;
        return salary + overtimeCompensation;
    }

    void display() override {
        cout << "Employee: " << name << " (ID: " << id << ")" << endl;
        cout << "Role: Developer" << endl;
        cout << "Base Salary: " << salary << endl;
        cout << "Overtime Compensation: " << extraHours * 500 << endl;
        cout << "Total Earnings: " << calculateEarnings() << endl;
    }
};

int main() {
    int employeeType;
    cout << "Enter Employee Type (1 for Manager, 2 for Developer): ";
    cin >> employeeType;

    if (employeeType < 1 || employeeType > 2) {
        cout << "Invalid employee type." << endl;
        return 0;
    }

    string name;
    int id;
    double salary;

    cout << "Enter Name: ";
    cin >> name;
    cout << "Enter ID: ";
    cin >> id;
    cout << "Enter Salary: ";
    cin >> salary;

    if (salary < 10000 || salary > 1000000) {
        cout << "Invalid salary." << endl;
        return 0;
    }

    if (employeeType == 1) {
        int rating;
        cout << "Enter Performance Rating (1-5): ";
        cin >> rating;

        if (rating < 1 || rating > 5) {
            cout << "Invalid rating." << endl;
            return 0;
        }

        Manager manager(name, id, salary, rating);
        manager.display();
    } else if (employeeType == 2) {
        int extraHours;
        cout << "Enter Extra Hours Worked: ";
        cin >> extraHours;

        if (extraHours < 0 || extraHours > 100) {
            cout << "Invalid extra hours." << endl;
            return 0;
        }

        Developer developer(name, id, salary, extraHours);
        developer.display();
    }

    return 0;
}
```
