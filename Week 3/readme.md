# 🏫 Galactic Academy Performance System

### Basic C++ OOP Challenge

---

## 📖 Background

The **Galactic Academy** trains different types of trainees for space missions.

Each trainee belongs to a specific training division.

The academy wants a simple software system to:

* Store trainee information
* Calculate final performance score
* Display trainee details

The academy management wants all trainees to be handled uniformly in the system, even though their performance calculation rules are different.

---

# 🎯 Objective

Write a C++ program that models different types of trainees and allows the academy to:

1. Calculate their final performance score
2. Display their details

The academy controller should be able to treat all trainees in the same way when calling the required functions.

---

# 🧑‍🚀 Common Trainee Information

Every trainee has:

* `int id`
* `string name`
* `double baseScore`

Each trainee must implement **ONLY TWO FUNCTIONS**:

```cpp
double calculateScore();
void display();
```

⚠️ No other functions are allowed.

---

# 🏅 Training Divisions

There are three types of trainees:

---

## 1️⃣ PilotTrainee

### Additional Data:

* `double flightHours`

### Score Rule:

Final Score = baseScore + (flightHours × 0.5)

---

## 2️⃣ EngineerTrainee

### Additional Data:

* `int projectsCompleted`

### Score Rule:

Final Score = baseScore + (projectsCompleted × 10)

---

## 3️⃣ ScientistTrainee

### Additional Data:

* `double researchHours`

### Score Rule:

Final Score = baseScore + (researchHours × 0.8)

---

# 📋 Program Requirements

* Create multiple trainees of different divisions.
* Store them together in a single list/array.
* The academy controller must:

  * Call `calculateScore()` for each trainee.
  * Call `display()` for each trainee.
* The controller should not depend on the specific division of trainee.
* Output should clearly show:

  * ID
  * Name
  * Final Score

---

# 🧠 Important Constraints

* Use only:

  * `int`
  * `double`
  * `string`
* Only **two functions** per class:

  * `calculateScore()`
  * `display()`
* No additional helper functions.
* Keep the design simple and clear.

---

# 📌 Sample Output (Example)

```
ID: 101
Name: Alex
Final Score: 85.5

ID: 102
Name: Mira
Final Score: 92.0
```

---

# 🏆 Evaluation Criteria

| Criteria                  | Marks |
| ------------------------- | ----- |
| Correct Score Calculation | 40    |
| Proper Design Structure   | 30    |
| Correct Function Behavior | 20    |
| Code Clarity              | 10    |

---

# 🚀 Goal

Design the system in such a way that:

> The academy can add new trainee divisions in the future without changing how it calls `calculateScore()` or `display()`.

---
