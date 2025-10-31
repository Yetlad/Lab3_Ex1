# Kotlin Employee Salary Calculator

This project demonstrates Object-Oriented Programming (OOP) principles in Kotlin by modeling different types of employees and calculating their respective salaries using inheritance and polymorphism.

## 🚀 Project Overview

The core of this project is built around the `Employee` base class, which is inherited by specific employee types (`FullTimeEmployee` and `PartTimeEmployee`). This setup allows for flexible and type-safe salary calculations.

### Key Features
* **Inheritance:** Uses a base class (`Employee`) with shared properties.
* **Polymorphism:** The `calculateSalary()` function is overridden in subclasses to implement specific pay logic.
* **Data Structure:** A Kotlin `mapOf` is used to store and iterate over multiple employee objects.

## 🛠️ Implementation Details

### Employee Structure

| Class | Key Property | Salary Calculation Logic |
| :--- | :--- | :--- |
| **Employee** (Base Class) | `baseSalary` (protected) | Returns `baseSalary`. |
| **FullTimeEmployee** | `bonus` (private) | `baseSalary` + `bonus` |
| **PartTimeEmployee** | `hourlyRate`, `hoursWorked` (private) | `hourlyRate` * `hoursWorked` |

### Kotlin Code (`main.kt`)

```kotlin
// 1. Base Class: Employee
open class Employee(
    protected val name: String,
    protected val baseSalary: Double
) {
    // Open function to be overridden by subclasses
    open fun calculateSalary(): Double {
        return baseSalary
    }

    // A helper function to display details
    fun displaySalary() {
        println("$name's salary: \$${"%.2f".format(calculateSalary())}")
    }
}

// 2. Subclass 1: FullTimeEmployee
class FullTimeEmployee(
    name: String,
    baseSalary: Double,
    private val bonus: Double
) : Employee(name, baseSalary) {
    
    // Override the function to include the bonus
    override fun calculateSalary(): Double {
        return baseSalary + bonus
    }
}

// 3. Subclass 2: PartTimeEmployee
class PartTimeEmployee(
    name: String,
    private val hourlyRate: Double,
    private val hoursWorked: Int
) : Employee(name, 0.0) { // Base salary is set to 0.0 as their main pay is hourly

    // Override the function to calculate pay based on hourly rate and hours
    override fun calculateSalary(): Double {
        return hourlyRate * hoursWorked
    }
}

// Main execution block
fun main() {
    // 4. Create a map of employees using mapOf
    val employees = mapOf(
        "Alice" to FullTimeEmployee("Alice Smith", 50000.0, 5000.0),
        "Bob" to FullTimeEmployee("Bob Johnson", 65000.0, 7500.0),
        "Charlie" to PartTimeEmployee("Charlie Brown", 20.0, 80),
        "Dana" to PartTimeEmployee("Dana White", 35.50, 45)
    )

    println("--- Employee Salary Report ---")
    // 5. Loop through the map and display each employee’s salary
    for ((_, employee) in employees) {
        employee.displaySalary()
    }
    println("------------------------------")
}
