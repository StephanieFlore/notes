#

___

**Memory Hierarchy (Performance)**

- **Registers**  - data on your desk (instant access)
- **Cache**      - next room
- **RAM**        - down the street
- **SSD**        - drive to another city
- **HDD**        - fly to another country

**Key Point**\
Memory access speeds differ by huge orders of magnitude

---

**Local vs. Global Variables**

`Local Variables`
- Live on the **stack**
- Only accessible **inside the block/function** where declared.
- Automatically destroyed when the function ends.

`Global Variables`
- Stored in the **global/ static memory segment** (not stack or heap)
- Exist for the **entire duration** of the program.
- Accessible from **any file/function** (if declared properly). 


**Constant vs. Static**

`Constant`
- Value **cannot change** after initialization.

  Example:
  
  `const int x = 5; → immutable`

**static (in a class)**
- Belongs to the class, not to individual objects.
- Can be used **without creating an object:**\
  `ClassName::method( )`

**static (in a function)**
- Remember its value **between function calls.**

Professor Clark EMPHASIZED:

`static` is **not equal** to `const`
Static is **not** about immutability. It is about **lifetime / class-level existence.**

---

# 2. Pointers, References, Parameters Passing


**Pointer**
- Holds *memory address*
- Can be a `nullptr`
- Syntax: `int* p`

**Reference**


`std::thread` Essentials

**Creating a thread:**
```c++
			std::thread t(myFunction, arg1, arg2)
			t.join( );
```

**Useful tools: **
- `std::this_thread::sleep_for(...)`
- `std::thread::hardware_concurrency( )`


**Parallel vs Concurrency**

**Parallel**
- Truly simultaneous on multiple cores.
**Concurrent**
- Tasks switch back and forth (time-slicing).

**Process vs Thread**

**Processes**
- Separate memory space
- Safe but heavy 
 -Communication via messages/pipes 

**Threads**
- Share memory
- Fast but dangerous
- Communication is done **shared memory**

**Race Conditions**\
Happens when:

- Two threads access the same data,
- At least one writes,
- No synchronization.


std::thread  Essentials
Creating a thread:
			std::thread t(myFunction, arg1, arg2)
			t.join( );

Useful tools;
 std::this_thread::sleep_for(...) 
 std::thread::hardware_concurrency( ) 

**Synchronization**

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

### Classes, Headers, Compilation, Linking

**Header File (.h)**
- Contains class definitions:
    - Member variables
    - Method signatures
- No full implementations

**Source File (.cpp)**
- Contains full method implementations

### Compilation + Linking Overview

**Preprocessor**
- Handles #include
- Literally copies header contents into the .cpp

**Compiler**
- Turns each .cpp into a separate object file (.o / .obj).

**Linker**
- Combines all objects files into the final executable.
- If something was declared but never defined → Linker error: “unresolved external”


### Forward Declaration

Example:
```c++
		Class JobSystem;
```
This tells the compiler: “This type exists; trust me.”\
Actual definition must appear in another .cpp or .h


### Virtual, Pure Virtual, V-Table, Destructors

**Virtual Functions**
- Allow runtime polymorphism.
- Derived classes override virtual functions.

**Correct:**
```c++
	virtual void makeSound( );
```

### Pure Virtual Function
Makes a class **abstract:**

```c++
	virtual void makeSound( ) = 0;
```

- Class cannot be instantiated.
- All subclasses **must** implement the function

**V-Table (Virtual Pointer Table)**

**What it is:**\
A table of function pointers that determine which overridden methods get called at runtime.

**What he’ll test:**
- If you call a method through a base pointer, the v-table ensures the **derived version** is called.


**Virtual Destructor**\
If the base class destructor is **not virtual**, deleting via a base pointer:
```c++
	Animal* a = new Dog( );
	delete a;

→ only Animal’s destructor runs → resource leak.
```

### Function Pointers, Functors, Lambdas

**Function Pointers**
- Point to functions.
- Used by threads, callbacks, and functional patterns.

**Functors (Function Objects)**
- Class with `operator( )` overloaded.

**Lambdas**
Basic form:
```c++
[] (int x) { return x + 1; }
```

**Captures:**

- [ ] 	  – capture nothing
- [ = ] 	– capture all by value 
- [ & ] 	– capture all by reference
- [ x ]	  – capture x by value
- [ &x ]	– capture x by reference




