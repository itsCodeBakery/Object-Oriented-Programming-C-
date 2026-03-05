
````markdown
# C++ OOP Quick Guide: Function Overloading & Inheritance Specifiers

This README is a beginner-friendly guide for **Function Overloading** and **Inheritance Access Specifiers** in C++.  
It includes **clear definitions** and **working examples** (including the common “function hiding” issue).

---

## 1) Function Overloading in C++

### Definition
**Function overloading** means defining **multiple functions with the same name** but with **different parameter lists**.

✅ Overloading can differ by:
- Number of parameters  
- Type of parameters  
- Order of parameter types  

❌ Overloading **cannot** differ only by return type.

---

### Example A: Simple Function Overloading (No Classes)

```cpp
#include <iostream>
using namespace std;

int add(int a, int b) { return a + b; }
double add(double a, double b) { return a + b; }
int add(int a, int b, int c) { return a + b + c; }

int main() {
    cout << add(2, 3) << endl;         // int version
    cout << add(2.5, 3.5) << endl;     // double version
    cout << add(1, 2, 3) << endl;      // 3-argument version
}
````

---

## 2) Function Overloading with Inheritance (Creative Example: Food Order System)

### Scenario

A restaurant has a basic ordering system and an online ordering system:

* **Restaurant** can take order of **one item**
* **OnlineRestaurant** can take:

  * **two items**
  * **item with quantity**

```cpp
#include <iostream>
using namespace std;

class Restaurant {
public:
    void order(string item) {
        cout << "Order received: " << item << endl;
    }
};

class OnlineRestaurant : public Restaurant {
public:
    // Overloaded order: two items
    void order(string item1, string item2) {
        cout << "Order received: " << item1 << " and " << item2 << endl;
    }

    // Overloaded order: item + quantity
    void order(string item, int quantity) {
        cout << "Order received: " << quantity << " " << item << endl;
    }
};

int main() {
    OnlineRestaurant customer;

    // customer.order("Burger");  // ⚠️ this causes an error due to function hiding (explained below)

    customer.order("Burger", "Pizza");
    customer.order("Biryani", 3);

    return 0;
}
```

---

## 3) IMPORTANT: Function Hiding in Inheritance (Common Student Error)

### Why this happens?

When a child class defines a function with the **same name** as the parent, it **hides ALL parent functions with that name**.

In the example above:

* Parent has: `order(string)`
* Child has: `order(string,string)` and `order(string,int)`

So `customer.order("Burger")` will fail because the parent version is hidden.

### Fix: Bring parent function into child scope

Add this line inside the child class:

```cpp
using Restaurant::order;
```

✅ Corrected code:

```cpp
#include <iostream>
using namespace std;

class Restaurant {
public:
    void order(string item) {
        cout << "Order received: " << item << endl;
    }
};

class OnlineRestaurant : public Restaurant {
public:
    using Restaurant::order;   // ✅ brings parent order() back into scope

    void order(string item1, string item2) {
        cout << "Order received: " << item1 << " and " << item2 << endl;
    }

    void order(string item, int quantity) {
        cout << "Order received: " << quantity << " " << item << endl;
    }
};

int main() {
    OnlineRestaurant customer;

    customer.order("Burger");            // ✅ now works
    customer.order("Burger", "Pizza");
    customer.order("Biryani", 3);

    return 0;
}
```

---

## 4) Inheritance Access Specifiers in C++

When you inherit a base class, you choose one of these:

```cpp
class Child : public Parent
class Child : private Parent
class Child : protected Parent
```

These control **how Parent’s members appear inside the Child** and whether the **outside world** can access them through a Child object.

---

### Parent Class Members Refresher

* `public`    → accessible everywhere
* `protected` → accessible inside class + derived classes
* `private`   → accessible only inside the same class

---

## 5) Differences: public vs private vs protected inheritance

### Access Conversion Rule

| Inheritance Type | Parent public becomes | Parent protected becomes | Accessible via Child object? |
| ---------------- | --------------------- | ------------------------ | ---------------------------- |
| `public`         | public                | protected                | ✅ public members accessible  |
| `private`        | private               | private                  | ❌ not accessible             |
| `protected`      | protected             | protected                | ❌ not accessible             |

> Note: Parent `private` members are **never directly accessible** in the child.

---

## 6) One Program Showing ALL THREE Inheritance Types

### Scenario

We have a base class `Camera`:

* `capture()` is public
* `adjustFocus()` is protected

Then three derived classes:

1. `SmartCamera : public Camera`
2. `SecuritySystem : private Camera`
3. `DroneCamera : protected Camera`

```cpp
#include <iostream>
using namespace std;

class Camera {
public:
    void capture() {
        cout << "Camera capturing photo..." << endl;
    }

protected:
    void adjustFocus() {
        cout << "Camera adjusting focus..." << endl;
    }
};

// 1) PUBLIC inheritance: IS-A relationship
class SmartCamera : public Camera {
public:
    void demo() {
        capture();      // ✅ ok
        adjustFocus();  // ✅ ok
    }
};

// 2) PRIVATE inheritance: implementation detail
class SecuritySystem : private Camera {
public:
    void monitor() {
        capture();      // ✅ ok inside
        adjustFocus();  // ✅ ok inside
    }
};

// 3) PROTECTED inheritance: only for inheritance chain
class DroneCamera : protected Camera {
public:
    void start() {
        capture();      // ✅ ok inside
        adjustFocus();  // ✅ ok inside
    }
};

int main() {
    SmartCamera sc;
    sc.capture();   // ✅ allowed (public inheritance)
    sc.demo();

    SecuritySystem ss;
    ss.monitor();
    // ss.capture(); // ❌ ERROR: capture became private in SecuritySystem

    DroneCamera dc;
    dc.start();
    // dc.capture(); // ❌ ERROR: capture became protected in DroneCamera

    return 0;
}
```

---

## 7) When to Use Which Inheritance Type?

### ✅ Use `public` inheritance when:

You want an **IS-A** relationship.

* `SmartCamera is a Camera`
* `Car is a Vehicle`

### ✅ Use `private` inheritance when:

You want to **reuse implementation** but **hide** the parent interface.

* `UserManager uses DatabaseConnection internally`

### ✅ Use `protected` inheritance when:

You want the parent interface available for **future subclasses**, but **not for outside users**.

* Useful in framework/base-library designs.

---



## Compile & Run

If you saved any example as `main.cpp`:

```bash
g++ main.cpp -o app
./app
```

---

## Common Mistake Checklist

✅ If calling parent function from derived object fails:

* Check if the derived class has a function with the same name (function hiding).
* Fix using:

```cpp
using ParentClass::functionName;
```

---


