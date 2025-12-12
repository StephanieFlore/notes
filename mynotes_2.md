## 1. Memory & Variables

### 1.1 Stack vs Heap

**Stack**
- **Used for:** local variables, function parameters, return addresses.
- **Lifetime:** automatically created when a function begins; destroyed when it ends.
- **Advantages:** very fast, memory handled automatically.
- **Disadvantages:** limited size; cannot dynamically resize; cannot outlive its scope.

**Heap**
- **Used for:** dynamically allocated memory (`new` / `malloc`).
- **Lifetime:** exists until explicitly released (`delete` / `free`).
- **Advantages:** flexible size, can create objects that outlive a function.
- **Disadvantages:** slower, requires manual management (can leak memory).

**In simple words:**
- Stack = **automatic**, fast, temporary workspace.
- Heap 	= **manual**, flexible, persistent storage while program runs.

### 1.2 Local vs. Global Variables

`Local Variables`
- Live on the **stack**
- Only accessible **inside the block/function** where declared.
- Automatically destroyed when the function ends.

`Global Variables`
- Stored in the **global/ static memory segment** (not stack or heap)
- Exist for the **entire duration** of the program.
- Accessible from **any file/function** (if declared properly). 

---

### 1.3 Constant vs. Static

`Constant`
- Value **cannot change** after initialization.
- Example: `const int x = 5;` → immutable`

**static (in a class)**
- Belongs to the class, not to individual objects.
- Can be used **without creating an object:**\
  `ClassName::method( )`

**static (in a function)**
- Remember its value **between function calls.**

Professor Clark EMPHASIZED:

`static` is **not equal** to `const`\
Static is **not** about immutability. It is about **lifetime / class-level existence.**

---

## 2. Pointers, References, Parameters Passing

### 2.1 Pointers vs. References

**Pointer**
- Holds **memory address**
- Can be a `nullptr`
- Syntax: `int* p`

**Reference**
- An alias to an existing variable.
- Must refer to a valid object.
- Cannot be null
- Syntax: `int& r`

**Key Idea**
- Passing an object **by reference guarantees** the **object exists.**
- Passing a raw pointer does **not guarantee that.**

---

### 2.2 Pass-by Value/ Reference/ Pointer

**Pass by Value**
- Function gets a **copy.**
- Does **not** modify the original.

**Pass by Reference `(&)`**
- Function gets an alias.
- Changes **affect the original variable.**

**Pass by Pointer `(*)`**
- Function receives a memory address.
- Can modify the original if the pointer is not null.

---

## 3 Arrays, Lists, and Data Structures

### 3.1 Arrays vs. Linked Lists

**Arrays**
- Contiguous memory.
- Very fast sequential access (cache-friendly).
- Better for indexing and iterating.

**Linked Lists**
- Nodes scattered in memory.
- Excellent for insertions/deletions in the middle.
- Bad sequential speed (cache-unfriendly).

**Quick Summary**
- Use arrays for performance + sequential access.
- Use linked lists for flexible insertion/removal.

---

### 3.2 Stack vs Queue

**Stack (LIFO)**

Examples:
- Undo history
- Call stack
- Backtracking

**Queue (FIFO)*

Examples:
- Task scheduling
- BFS traversal
- Print jobs

---

## 4. Classes, Headers, Compilation, Linking

**4.1 .h and .cpp**

**Header File (.h)**
- Contains **class definitions:**
	- member variables
	- method signatures
- NO full implementations.

**Source File (.cpp)**
- Contains full method **implementations.**

---

### 4.2 Compilation + Linking Overview

**Preprocessor**
- Handles `#include`
- Literally **copies** header contents into the `.cpp`

  **Compiler**
  - Turns each `.cpp` into a **separate object file** `(.o/ .obj)`
 
  **Linker**
  - Combines all objects files into the **final executable**
  - If sometthing was declared byt never defined → **Linker error: "unresolved external".**

  **Forward Declaration**

  Example:
```c++
class JobSystem;
```

This tells the compliler: "This types exists; trust me."\
Actual definition must appear in another `.cpp` or `.h`.

## 5. OOP: Virtual, V-Table, Destructors

### 5.1 Virtual Functions
- Allow runtime polymorphism
- Derived classes override virtual functions

Example:
```c++
virtual void makeSound();
```

### 5.2 Pure Virtual Function
Makes a class **abstract**

```c++
virtual void makeSound() = 0;
```
- Class cannot be instantiated.
- All subclasses **must** implement the function.

---

### 5.3 V-Table (Virtual Pointer Table)

**What it is:**\
A table of function pointers that determine which overridden methods get called at runtime.

**What he'll test:*\
- If you call a method through a base pointer, the v-table ensures that **derived version** is called.

### 5.4 Virtual Destructor

If the base class destructor is **not virtual**, deleting via a base pointer:
```c++
	Animal* a = new Dog( );
	delete a;

→ only Animal’s destructor runs → resource leak.
```

 ---

 ## 6. Function Pointers, Functors, Lambdas

**Function Pointers**
- Point to functions.
- Used by threads, callbacks, and functional patterns.

**Functors (Function Objects)**
- Class with `operator( )` overloaded.

**Lambdas**\
Basic form:
```c++
[] (int x) { return x + 1; }
```

**Captures:**

– []	- capture nothing
- [=]	– capture all by value 
- [&] 	– capture all by reference
- [x]	– capture x by value
- [&x]	– capture x by reference

---

## 7. Threads, Processes, Synchronization
    
### 7.1 Parallel vs. Concurrency

**Parallel**
- Truly simultaneous on multiple cores.
**Concurrent**
- Tasks switch back and forth (time-slicing).

---

### 7.2 Process vs. Thread**

**Processes**
- Separate memory space
- Safe but heavy 
 -Communication via messages/pipes 

**Threads**
- Share memory
- Fast but dangerous
- Communication is done **shared memory**

---

### 7.3 Race Conditions*\
Happens when:

- Two threads access the same data,
- At least one writes,
- No synchronization.

---

### 7.4 `std::thread` Essentials

Creating a thread:
```c++
std::thread t(myFunction, arg1, arg2)
t.join( );
```

Useful tools:
- `std::this_thread::sleep_for(...)`
- `std::thread::hardware_concurrency( )`

---

### 7.5 Synchronization

**Mutex**
```c++
std::mutex m;
m.lock();
// critical selection
m.unlock() ;
```

**Lock_guard**
```c++
std::lock_guard<std::mutex> lock (m)
// automatically unlocks at end of scope
```

**Atomics**
- For primitive types (int, bool).
- Very fast, lock-free operations
- NOT for large objects

When to use:
- Use **atomic** for simple counters/flags
- Use **mutex/lock_guard** for protecting complex data 

---

## 8. Memory Hierarchy (Performance)

Analogy from professor:
- **Registers**  - data on your desk (instant access)
- **Cache**      - next room
- **RAM**        - down the street
- **SSD**        - drive to another city
- **HDD**        - fly to another country

**Key Point**\
Memory access speeds differ by huge orders of magnitude
