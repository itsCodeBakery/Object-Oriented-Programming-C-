
# Inheritance in C++: A Comprehensive Guide

Inheritance is one of the "big four" pillars of Object-Oriented Programming (OOP). It allows you to create a new class (child) based on an existing class (parent), inheriting its attributes and behaviors.

---

## 1. What is Inheritance?

In simple terms, inheritance is about **reusability**. Instead of writing the same code over and over for different objects, you can create a general class and then create more specific versions of it.

* **Base Class (Parent):** The existing class you are inheriting from.
* **Derived Class (Child):** The new class that inherits the features.

---

## 2. Basic Syntax

To inherit from a class, use the colon (`:`) symbol followed by an access specifier (usually `public`).

```cpp
class Parent {
    // Parent members
};

class Child : public Parent {
    // Child inherits Parent members and can add its own
};

```

---

## 3. Subtyping vs. Specialization

While these terms are often used interchangeably, they describe different ways we think about inheritance:

### Subtyping (The "Is-A" Relationship)

Subtyping means that the derived class can be used anywhere the base class is expected. It’s about **compatibility**.

* **Example:** A `Dog` is a subtype of `Animal`. If a function needs an `Animal`, you can safely give it a `Dog`.

### Specialization

Specialization is about **adding detail**. The derived class is a "special" version of the base class that has more specific data or different behavior.

* **Example:** A `Vehicle` is a general concept, but a `RaceCar` is a specialized version with a nitro boost and aerodynamic features.

---

## 4. Access Specifiers in Inheritance

When you inherit, you decide how "visible" the parent's members will be in the child class:

| Access Specifier | Description |
| --- | --- |
| **Public** | Public members of the parent stay public in the child. Most common. |
| **Protected** | Members are accessible within the parent and child classes, but not from the outside. |
| **Private** | All inherited members become private in the child class. |

---

## 5. Code Example

Here is a simple program showing how a `Car` inherits from a `Vehicle`.

```cpp
#include <iostream>
#include <string>
using namespace std;

// Base Class (Parent)
class Vehicle {
public:
    string brand = "Ford";
    void honk() {
        cout << "Tuut, tuut! \n";
    }
};

// Derived Class (Child) - Specialization
class Car : public Vehicle {
public:
    string model = "Mustang";
};

int main() {
    Car myCar;
    
    // Using inherited method and attribute
    myCar.honk();
    cout << myCar.brand << " " << myCar.model << endl;
    
    return 0;
}

```

---


---

> **Note:** Always remember that inheritance should represent a logical relationship. Don't use it just to save a few lines of code; use it because the child truly "is a" version of the parent!

---

