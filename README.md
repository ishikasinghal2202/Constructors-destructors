

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


## Algorithm:
1. Define a class.
2. Declare multiple constructors with different parameter lists.
3. Implement each constructor with specific initialization logic.
4. Create objects using different sets of arguments.
5. Compiler selects the appropriate constructor based on arguments.
6. Ensure no ambiguity among overloaded constructors.


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



## CONCLUSION:

    - Constructors help initialize objects automatically in various ways.
    - Destructors ensure safe cleanup of resources.
    - Copy and Move semantics allow flexible and efficient object handling.
    - Rule of 3/5/0 guides when to implement special member functions.
    - RAII ensures resource safety and exception-proof code.

