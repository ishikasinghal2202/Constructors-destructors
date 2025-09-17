

## AIM:
    To study and implement Constructors and Destructors Programs in C++.

## SOFTWARE USED:
    - Visual Studio Code (VS Code)
    - g++ compiler (C++17 or later)

## OBJECTIVES:
    - Understand object lifecycle in C++ (creation → use → destruction).
    - Implement default, parameterized, copy, and move constructors.
    - Understand destructors and their role in resource management.
    - Learn Rule of 3/5/0 and RAII principle.
    - Identify common pitfalls (shallow copies, missing virtual destructor, etc.).


## THEORY 

### 1) Constructor:
   - Special member function, same name as class, no return type.
   - Used to initialize objects automatically at creation.
   - Types:
        • Default Constructor
        • Parameterized Constructor
        • Copy Constructor
        • Move Constructor
        • Delegating & Explicit Constructors
   - Best practice: Use initializer lists for efficiency.

### 2) Destructor:
   - Special member function prefixed with '~' (e.g., ~Class()).
   - Called automatically when object goes out of scope.
   - Used to release memory/resources.
   - Must be virtual if class is used polymorphically.

### 3) Rule of Three / Five / Zero:
   - If class defines one of destructor, copy ctor, copy assignment → needs all three.
   - Rule of Five (C++11): Add move ctor and move assignment.
   - Rule of Zero: Prefer STL/RAII classes to avoid manual management.

### 4) RAII (Resource Acquisition Is Initialization):
   - Acquire resources in constructor.
   - Release them in destructor.
   - Guarantees cleanup even with exceptions.

### 5) Pitfalls:
   - Shallow copy leads to double free or memory leaks.
   - Forgetting virtual destructors in base classes.
   - Heavy constructor work without exception-safety.


 ### PROGRAM EXAMPLES:
#include <iostream>
#include <string>
#include <cstring>
using namespace std;

#### Example A 
// Default, Parameterized, Destructor
class Student {
    int id;
    string name;
public:
    // Default Constructor
    Student() : id{0}, name{"Unknown"} {
        cout << "Default Constructor called\n";
    }

    // Parameterized Constructor
    Student(int i, string n) : id{i}, name{move(n)} {
        cout << "Parameterized Constructor called\n";
    }

    // Destructor
    ~Student() {
        cout << "Destructor called for " << name << "\n";
    }

    void show() const {
        cout << id << " : " << name << endl;
    }
};

#### Example B 
// Copy Constructor, Move Constructor, Rule of Five
class Buffer {
    char* data;
    size_t size;
public:
    // Default
    Buffer() : data{nullptr}, size{0} {}

    // Parameterized
    explicit Buffer(const char* s) {
        size = strlen(s);
        data = new char[size+1];
        memcpy(data, s, size+1);
        cout << "Parameterized Buffer created\n";
    }

    // Copy Constructor (deep copy)
    Buffer(const Buffer& other) : size{other.size} {
        data = new char[size+1];
        memcpy(data, other.data, size+1);
        cout << "Copy Constructor called\n";
    }

    // Copy Assignment
    Buffer& operator=(const Buffer& other) {
        if(this != &other) {
            delete[] data;
            size = other.size;
            data = new char[size+1];
            memcpy(data, other.data, size+1);
            cout << "Copy Assignment called\n";
        }
        return *this;
    }

    // Move Constructor
    Buffer(Buffer&& other) noexcept : data{other.data}, size{other.size} {
        other.data = nullptr;
        other.size = 0;
        cout << "Move Constructor called\n";
    }

    // Move Assignment
    Buffer& operator=(Buffer&& other) noexcept {
        if(this != &other) {
            delete[] data;
            data = other.data;
            size = other.size;
            other.data = nullptr;
            other.size = 0;
            cout << "Move Assignment called\n";
        }
        return *this;
    }

    // Destructor
    ~Buffer() {
        delete[] data;
        cout << "Buffer Destructor called\n";
    }

    void print() const {
        if(data) cout << "Data: " << data << endl;
        else cout << "Empty Buffer\n";
    }
};

// ------------------------------ Main ------------------------------
int main() {
    cout << "\n--- Example A: Student Class ---\n";
    Student a;            // Default constructor
    Student b(101, "Ava");// Parameterized constructor
    a.show();
    b.show();

    cout << "\n--- Example B: Buffer Class ---\n";
    Buffer buf1("Hello C++");
    buf1.print();

    cout << "\nCopying buf1 to buf2:\n";
    Buffer buf2 = buf1; // Copy constructor
    buf2.print();

    cout << "\nMoving buf1 to buf3:\n";
    Buffer buf3 = move(buf1); // Move constructor
    buf3.print();
    buf1.print(); // Now empty

    cout << "\nAssignment operations:\n";
    Buffer buf4;
    buf4 = buf2;  // Copy assignment
    buf4.print();

    Buffer buf5;
    buf5 = move(buf2); // Move assignment
    buf5.print();
    buf2.print();

    cout << "\n--- End of Program ---\n";
    return 0;
}


## CONCLUSION:

    - Constructors help initialize objects automatically in various ways.
    - Destructors ensure safe cleanup of resources.
    - Copy and Move semantics allow flexible and efficient object handling.
    - Rule of 3/5/0 guides when to implement special member functions.
    - RAII ensures resource safety and exception-proof code.

