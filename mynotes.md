# Pre-Test 

## Section 1: Object-Oriented Programming Concepts 

### 1.1 Inheritance and Polymorphism

Consider a vehicle hierarchy where you have a base `Vehicle` class and derived classes `Car` and `Truck`.

**a) Write pseudocode for a base** `Vehicle` **class that has:**
- An abstract method `calculateFuelEfficiency()`
- A concrete method `startEngine()` that prints "Engine started"

First of all,

**What is an Abstract Method?**

An **abstract method** is a method that has *no code inside it yet.*
It is like a **placeholder** or a **promise** that *every child class must fill in.*

**You declare it, but you do NOT define how it works.**

Example:
```java
public abstract double calculateFuelEfficiency();
```
There is **no body**, no `{ }`, because the method has no implementation yet.

**Key Points:**
- Abstract methods only appear in **abstract classes**.
- You **cannot** create an object of an abstract class.
- Any class that extends it **must override** the abstract method.

**What is a Concrete Method?**

A **concrete method** is a method that *already has code written inside it.*
It has a full implementation and can be used as is by its subclasses.

Example:
```java
public void startEngine() {
    System.out.println("Engine started");
}
```

**Key Points**
- Concrete methods can exist in **regular** classes or **abstract** classes.
- They **already work**, so child classes inherit them automatically.
- Subclasses can use them without writing any additional code.

**Quick Summary**

| Term            | Meaning       | Has Code?     | Must Child Override? |
| -------------   | ------------- | ------------- | -------------------- |
| Abstract Method | A method with no implementation  |  No  |  Yes |
| Concrete Method | A method that already works  |  Yes  |  No  |


Here is the solution to the question:

Base Class: Vehicle
```java
// Vehicle.java
public abstract class Vehicle {

    // Abstract method - no body, subclasses must override
    public abstract double calculateFuelEfficiency();

    // Concrete method - already implemented
    public void startEngine() {
        System.out.println("Engine started");
    }
}
```

*OPTIONAL* - Derived Class: Car
```java
public class Car extends Vehicle {

    @Override
    public double calculateFuelEfficiency() {
        // Example: return miles per gallon for a car
        return 30.0;
    }
}
```

*OPTIONAL* - Derived Class: Truck
```java
public class Truck extends Vehicle {

    @Override
    public double calculateFuelEfficiency() {
        // Example: return miles per gallon for a truck
        return 15.0;
    }
}
```

*OPTIONAL* - Example of Using These Classes
```java
public class Main {
    public static void main(String[] args) {
        Vehicle myCar = new Car();
        Vehicle myTruck = new Truck();

        myCar.startEngine();
        System.out.println("Car MPG: " + myCar.calculateFuelEfficiency());

        myTruck.startEngine();
        System.out.println("Truck MPG: " + myTruck.calculateFuelEfficiency());
    }
}
```

In Conclusion,
- `Vehicle` is **abstract**, meaning you **cannot** make a Vehicle object.
- `calculateFuelEfficiency()` is **abstract**, meaning every subclass must write its own version.
- `startEngine()` is **concrete**, meaning all vehicles inherit it automatically.
- `Car` and `Truck` **extend Vehicle**, so they automatically get `startEngine()` and must override `calculateFuelEfficiency()`.

---

**b) Explain the difference between method overriding and method overloading. Give an example of when you would use each.**

**What is Method Overriding and Method Overloading?**

**Method Overriding** - *"Same question, different answers"*
This is when a parent class has a method, and the child class gives **its own version** of that method.

Example:
```
Your mom says: “This is how you clean your room.”
You say:       “Well, this is my way of cleaning my room.”

Same task → different versions.
```
You use `Overriding` when **different objects must do the same things differently.**

**Method Overloading** - *"Same name, different ways to use it"*
This is when a class **has multiple methods with the same name**, but they take **different kinds of input.**

Example:
```
Imagine a "draw" method: 

- draw(circle)
- draw(square, size)
- draw(color, shape)

Same word "draw," but you can use it in different ways depending on what you give it.
```
You use `Overloading` when you want to do similar actions, but with different options.

---

**c) If** `Vehicle v = new Car()` **, what happens when you call** `v.calculateFuelEfficiency()` **? Explain the mechanism that makes this work?**




