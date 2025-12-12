# Pre-Test 

## Section 1: Object-Oriented Programming Concepts 

### 1.1 Inheritance and Polymorphism

Consider a vehicle hierarchy where you have a base `Vehicle` class and derived classes `Car` and `Truck`.

**a) Write pseudocode for a base** `Vehicle` **class that has:**
- An abstract method `calculateFuelEfficiency()`
- A concrete method `startEngine()` that prints "Engine started"

First of all,

**What is an Abstract Method?**

An **abstract method** is a method that has *no code inside it yet.*\
It is like a **placeholder** or a **promise** that *every child class must fill in.*

**You declare it, but you do NOT define how it works.**

Example:
```java
public abstract double calculateFuelEfficiency();
```
There is **no body**, **no `{ }`**, because the method has no implementation yet.

**Key Points:**
- Abstract methods only appear in **abstract classes**.
- You **cannot** create an object of an abstract class.
- Any class that extends it **must override** the abstract method.

**What is a Concrete Method?**

A **concrete method** is a method that *already has code written inside it.*\
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
| **Abstract Method** | A method with no implementation  |  No  |  Yes |
| **Concrete Method** | A method that already works  |  Yes  |  No  |


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

To Conclude,
- `Vehicle` is an **abstract class**, meaning you **cannot** make a Vehicle object.
- `calculateFuelEfficiency()` is an **abstract method**, meaning every subclass must write its own version.
- `startEngine()` is a **concrete class**, meaning all vehicles inherit it automatically.
- `Car` and `Truck` **extend Vehicle**, so they automatically get `startEngine()` and must override `calculateFuelEfficiency()`.

---

**b) Explain the difference between method overriding and method overloading. Give an example of when you would use each.**

**What is Method Overriding and Method Overloading?**

**Method Overriding** - *"Same question, different answers"*\
This is when a parent class has a method, and the child class gives **its own version** of that method.

Example:
```
Your mom says: “This is how you clean your room.”
You say:       “Well, this is my way of cleaning my room.”

Same task → different versions.
```
You use `Overriding` when **different objects must do the same things differently.**

**Method Overloading** - *"Same name, different ways to use it"*\
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

**Here is the solution to the question:**

Even though the variable is of type **Vehicle**, the **actual object** is a **Car**, so the **Car's version** of `calculateFuelEfficiency()` is the one that runs.

This works because of **dynamic binding** (also called **runtime polymorphism**).

**Here is an easy explanation:**

STEP 1 - The variable type
```java
Vehicle v
```
This means:
```
"v can point to any Vehicle or any subclass of Vehicle."
```
STEP 2 - The object created
```java
new Car()
```
This means that **the actual object in memory** is a Car.

So together:
```java
Vehicle v = new Car();
```
v = reference\
Car() = actual object

STEP 3 - What happens when you call:
```java
v.calculateFuelEfficiency();
```
Java looks at the **actual object type**, not the variable type.

So Java asks:
```
"v is currently pointing to a Car, so I will run the Car's version of the method."
```

Therefore,\
**The Car's** `calculateFuelEfficiency()` **method is executed.**

**Why does this happen? What is the mechanism that makes this work?**\
This works because of a feature called:

**Dynamic Binding or Runtime Polymorphism**

This means:\
When you call a method on a reference, **Java decides which version to run at runtime**, based on the **actual object**, NOT the reference type.

Here is a simple analogy to help you understand:
```
Imagine "Vehicle" is a job title, and "Car" is a specific employee.

You give an order:\
    "Hey Vehicle, calculate fuel efficiency!"
But the actual person standing there is **Car**, so **Car** will do the job.
```

**Quick Summary**
- `Vehicle v = new Car();` means the reference is Vehicle, but the object is Car.
- Java uses dynamic binding to figure out which method to call.
- Since the object is a Car, it runs Car's overridden calculateFuelEfficiency() method.

---

### 1.2 Memory Management Concepts

**a) Explain the difference between stack and heap memory allocation. Give an example of data that would typically be stored in each.**

Imagine your computer has two special “storage areas” in its brain:

`Stack` – The neat, organized shelf\
`Heap` – The big, messy toy box

**What is a Stack?**\
The **stack** is like a small shelf where things are stored in a very organized way.
- You can only put something on the **top** of the shelf.
- You can only take something from the top.
- Everything happens **fast** because it’s so organized.

**What Get Stored Here?**\
Things that don’t stay around very long – like:
- Local variables inside of a function 

Example: 
```java
int x = 5; (inside a method)
```
These disappear when the method is done just like toys you only play with for a moment.

`Heap` – The big, messy toy box
The **heap** is like a huge toy box.

You can put things inside whenever, wherever, and take them out in any order.
- It’s much bigger than the stack.
- But because it’s messier, it’s slower to find stuff.

**What Gets Stored Here?**\
Things that need to stay around longer or are created with `new`, like:
- Objects (Car, Dog, Student, etc.)
- Arrays
- Anything you want to use even after a method ends

Example: 
```java
Car myCar  =  new Car( )
```
The `Car` object is stored in the **heap.**

**Stack Memory Allocation**
The **stack** is a region of memory that stores data with a very strict and organized order. It operates in a Last-In, First-Out (LIFO) manner.

- Extremely fast access
- Automatically managed (memory is freed when a function ends)
- Stores short-lived data

**This is What is Typically stored on the Stack:**
- Local variables inside functions
- Function parameters
- Return addresses

Example:
```java
void stackExample( )  {
    int count = 5 ;		// stored on the stack
}
```

**Heap Memory Allocation**
The **heap** is a large, more flexible region of memory used for data that needs to live longer or has a dynamic size.
- Manually managed (you allocate with `new` and later deallocates or rely on garbage collection)
- Slower to access
- Used for **objects** or **data whose size you don’t know ahead of time**

**This is What is Typically stored on the Heap:**
- Objects created with `new`
- Arrays
- Data structures like lists, trees, hash maps, etc.

Example:
```java
Car myCar  =  new Car( ) ;	// the Car object lives on the heap
```
`myCar` stays in memory until the program is done with it or the garbage collector removes it.

---

**b) What is the difference between a local variable and a global variable in terms of:**

- **Scope**
- **Lifetime**
- **Memory Location**

`Local Variable`

**Scope**
- Only accessible *inside* the function, method, or block where it is declared. 
- You **cannot** use it outside that specific area.\
**Lifetime**
- Exists **only while the function is running.**
- Once the function is finished, the variable is destroyed.\
**Memory Location**
- Typically stored on the **stack**, because they are short-lived and automatically managed.

`Global Variable`

**Scope**
- Accessible from **any part of the program**, unless restricted by access modifiers or namespaces.

**Lifetime**
- Exists for the **entire duration of the program.**
- It is created when the program starts and destroyed when the program ends.

**Memory Location**
- Stored in a **fixed memory area** (often called the global/static data segment), not on the stack or heap. 
- This allows them to persist for the whole program.

**Quick Summary Table**

| Feature       | Local Variable    | Global Variable    |
| ------------- | ----------------- | ------------------ |
| **Scope**     | Inside the Function/ Block only    | Accessible Anywhere |
| **Lifetime**  | Only while the Function runs | Whole Program Runtime |
| **Memory**    | Stack             | Global/ Static region |

---

### 1.3 Parameter Passing

**a) Explain the difference between passing by value and passing by reference. When would you use each?**

**Passing by Value**
- You give a copy of the data to the method.
- Changes inside the method **do NOT affect** the original variable.
- Think of it like giving someone a **photocopy of your homework**. They can scribble on it, but your original stays the same.

Example:
```java
```

**When to Use:**
- Use this when you don’t want the method to change the original data.

**Passing Reference**
- You give the **actual variable** (or a reference to it) to the method.
- Changes inside the method **do affect** the original variable.
- Think of it like giving someone your **actual notebook**. Anything they write is in your notebook.

Example:
```java
```

**When to Use:**
Use this when you **want the method to modify the original data**, like updating an object or a list.

---

**b) In Java, when you pass an object to a method, what actually gets passed? How does this affect what you can do inside the method?**

**What Actually Gets Passed?**\
When you pass an object to mathod in Java, you are **not giving the method the whole object**.

You are giving the method a **copy of the directions to find the object.**

Think of it like this:
- The object is a **house.**
- The variable that points to the object is the **address** of the house.
- When you pass the object to a method, you are giving the method a **copy of the address**, not the house itself.

So the method knows **where the house is**, and it can go inside and make changes.

**How does this affect what you can do inside the method?**\

Because the method receives a **copy of the address**, it can:

- **Change what's inside the house**
    - For example, if the object has a name, the method can change that name.\
    - This change will be seen outside the method because you're changing the            *same* house.
- **Change which house the outside variable points to**
    - If the method tries to use a **different address**, this change **does not**
      affect the original variable.

---

### 1.4 Static Members

**a) Explain what a static variable is and how it is unique**

Imagine a classroom where every student has their **own notebook.**\
Those are **regular variables–** each person gets their own copy.

Now imagine the class has **ONE big whiteboard** at the front of the room.\
Everyone in the class can **see it**, **use it**, and **change it.**

That whiteboard is a **static variable.**

**So a** `Static Variable` **is:**
- **Shared by ALL objects** of that class
- There is **only one copy**, no matter how many objects you make
- If one object changes it, **everyone sees the change**

It’s unique because **it belongs to the class itself**, not to each individual object.

---

**b) Write pseudocode showing a** `Counter` **class with a static variable that tracks how many Counter objects have been created.**

Here is a simple pseudocode example using the same "whiteboard" idea:

```java
// Counter class
class Counter {

    // Static variable shared by ALL Counter objects
    static count = 0

    // Constructor
    constructor() {
        // Increase the count every time a new Counter object is made
        count = count + 1
    }

    // Method to show how many objects exist
    method showCount() {
        print("Total counters made: " + count)
    }
}
```

Explanation:
- The static variable `count` is like a **big scoreboard** on the wall.
- Every time you create a new Counter object, it says:\
      **"Hey, add 1 to the scoreboard!"**
- All Counter objects look at the **same scoreboard**, not their own.

---

## Section 2: Data Structures Analysis

### 2.1 Data Structure Selection

**For each scenario, choose the most appropriate data structure and explain why:**

**a) Implementing an undo feature in a text editor**
- **Data Structure:** Stack
- **Justification:**

  A stack works like a **pile of books.** You alwyas remove the book you             placed **last.**

  Undo works the same way:
  
  The **last action you did** is the **first one you undo.** That's why a stack is
  perfect.

**b) Storing key-value pairs for a phone directory where you need fast lookups by name**
- **Data Structure:** HashMap (or Hash Table)
- **Justification:**

  A HashMap is like a **magical dictionary** where you can find things super fast.\
  You look up a person’s name and instantly get their phone number.\
  It gives **fast search**, much faster than scanning a list\

**d) Representing a family tree with relationships between family members**
- **Data Structure:** Tree
- **Justification:**

  A tree looks like a real family tree:
  - Parents at the top
  - Children connected below
  - You can clearly show relationships
  
  It's perfect for representing **who is related to who.**

**e) Storing a list of students where you frequently need to add/remove students from the middle of the list**
- **Data Structure:** Linked List
- **Justification:**

  A linked list is like a **chain of people holding hands.**\
  If you want to add or remove someone in the middle, you just tell two people to
  hold different hands — very easy.

  In an **array**, you’d have to **move everyone over**, which is slow.\
  In a **linked list**, you only fix a couple of links.

---

### 2.2 Linked List Implementation
Write pseudocode for a simple singly linked list node structure and implement an `insert` method that adds a new element at the beginning of the list.

```java
```

---

### 2.3 Data Structure Trade-Offs

**a) Compare arrays and linked lists. For each structure, give one advantage and one disadvantage:**

**Array advantage:**
Arrays let you **get to any item really fast** because everything is stored next to each other, like seats in a movie theater.\
You know the seat number → you can jump straight to it.

**Array disadvantage:**
Arrays **can’t easily grow or shrink.** If you want to add or remove something in the middle, you often have to **move a bunch of items around**, which is slow.

**Linked list advantage:**
Linked lists make it **easy to add or remove items anywhere.**\
Each item just points to the next one, like kids holding hands in a line — you can insert a new kid without shifting everyone.

**Linked list disadvantage:**
Linked lists are **slow to look things up** because you must start at the beginning and walk through each node one by one.\
You **can’t jump** to an item directly like you can in an array.

---

## Section 3: Access Control and Encapsulation

### 3.1 Access Modifiers

**a) Explain the purpose of private, protected, and public access modifiers.**\
Think of access modifiers like **locks on doors** in a house. They control **who is allowed to go inside** (who can access variables/ methods)

**Private**\
**Who can access it?**\
- Only the **same class**\
**Purpose:**\
- To hide and protect data so no one else can touch it directly.
- Prevents accidental changes from outside the class.
**Easy idea:**
- Like your **diary.** Only *you* can open it.

**Protected**\
**Who can access it?**\
- The **same class**
- Any **subclass (child class)**
- Classes in the **same package**
**Purpose:**
- To allow child classes to use and extend behavior, but still keep it somewhat restricted.
**Easy idea:**
- Like a **shared family room.** Your family (child classes) can enter, but strangers cannot.

**Public**\
**Who can access it?**
- **Anyone**, from anywhere in the program.
**Purpose:**
- To make something openly available to use.
**Easy idea:**
- Like a **public park**. Everyone can go in.

**Summary Table**

| Modifier      | Who Can Access It?    | Simple Explanation    |
| ------------- | --------------------- | --------------------- |
| **Private**   | Same class only       | "Only I can use it."  |
| **Protected** | Same class + subclasses + same package | "My family can use it too." |
| **Public**    | Anyone                | "Everyone can use it."|

---

**b) Why would you make member variables private and provide public getter/setter
methods instead of making the variables public directly?**\
The main reason is **encapsulation** - protecting how data is accessed and changed.

Here's what that means:

**1. Control How the Data is Changed**\
If variables were public, anyone could change them to anythin at any time:

```java
person.age = -10;    // This should NOT be allowed!
```
By making the variables private and using a setter, you can **check** values before accepting them:
```java
public void setAge(int a) {
    if (a >= 0) {
        age = a;
    }
}
```
This keeps your object from getting into a "broken" state.

Now, let's shift our focus to a different point..

**Why is the setter method (setAge) public instead of private?**\
Because:

- **Private variables** mean only the class itself can directly touch the data.
- But if the variable is private, the only way for code outside the class to change it is through a **public** method.

So the rule is:
- Variables = private
- Getter/setter methods = public

Why?

Because if the setter were **private**, nobody outside the class could use it — meaning **no one could change the variable at all**, which defeats the purpose of having a setter.

Alright, let's circle back to our main point..

**2. Hide the Internal Details**\
Private variables let you hide how the data is stored inside the class.

If you ever decide to change your internal structure, the rest of your program **doesn't break** because everyone interacts through the same getter/setter methods

**3. Read-Only Or Write-Only Control**\
Maybe you want someone to see a value but not change it, or change it but not see it.

Getters/ Setters let you decide:
- Provide a **getter only** (read-only)
- Provide a **setter only** (write-only)
- Provide both (read/write)

**4. Add Extra Behavior**
You can add logic inside getters/ setters:

- Logging changes
- Validating data
- Automatically updating related values
- Without changing how the class is used.

---

### 3.2 Class Design
Design a simple `BankAccount` class that demonstrates good encapsulation practices. List the member variables and methods you would include, along with their access modifiers.






