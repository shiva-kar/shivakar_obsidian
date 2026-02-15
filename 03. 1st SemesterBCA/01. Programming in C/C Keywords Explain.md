## FUNDAMENTAL DATA TYPES

### `void`

**Definition:** Represents absence of value or type.

**Correct**

```c
void func(void) { }
```

**Wrong**

```c
void x = 10;   // invalid
```

**Scenario:** Functions that return nothing; generic pointers.

---

### `char`

**Definition:** Smallest addressable integer type, used for characters.

**Correct**

```c
char c = 'A';
```

**Wrong**

```c
char c = "A";   // string literal
```

**Scenario:** Text, raw bytes.

---

### `int`

**Definition:** Integer arithmetic type.

**Correct**

```c
int x = 10;
```

**Wrong**

```c
int x = 10.5;   // implicit truncation (conceptually wrong in exams)
```

**Scenario:** Counting, indexing, arithmetic.

---

### `float`

**Definition:** Single-precision floating-point type.

**Correct**

```c
float f = 3.14f;
```

**Wrong**

```c
float f = "3.14";
```

**Scenario:** Memory-efficient real numbers.

---

### `double`

**Definition:** Double-precision floating-point type.

**Correct**

```c
double d = 3.14159;
```

**Wrong**

```c
double d = 'A';
```

**Scenario:** Higher precision calculations.

---

### `_Bool`

**Definition:** Boolean type storing 0 or 1.

**Correct**

```c
_Bool b = 1;
```

**Wrong**

```c
_Bool b = 5;   // stored as 1, logically wrong
```

**Scenario:** Logical state representation.

---

### `_Complex`

**Definition:** Represents complex number type.

**Correct**

```c
double _Complex z;
```

**Wrong**

```c
_Complex x = 5;   // incomplete type usage
```

**Scenario:** Mathematical complex arithmetic.

---

### `_Imaginary`

**Definition:** Imaginary-only numeric type.

**Correct**

```c
double _Imaginary y;
```

**Wrong**

```c
_Imaginary i = "i";
```

**Scenario:** Specialized numeric computation.

---

## INTEGER MODIFIERS

### `short`

**Definition:** Integer type no larger than `int`.

**Correct**

```c
short s = 10;
```

**Wrong**

```c
short s = 1000000;   // overflow
```

**Scenario:** Memory-constrained integers.

---

### `long`

**Definition:** Integer type no smaller than `int`.

**Correct**

```c
long l = 100000L;
```

**Wrong**

```c
long l = "100";
```

**Scenario:** Larger integer range.

---

### `signed`

**Definition:** Allows negative and positive values.

**Correct**

```c
signed int x = -5;
```

**Wrong**

```c
signed unsigned int x;   // invalid
```

**Scenario:** Explicit signedness.

---

### `unsigned`

**Definition:** Allows only non-negative values.

**Correct**

```c
unsigned int x = 10;
```

**Wrong**

```c
unsigned int x = -1;
```

**Scenario:** Bitwise and range expansion.

---

## USER-DEFINED TYPES

### `struct`

**Definition:** Groups heterogeneous data under one name.

**Correct**

```c
struct A { int x; char y; };
```

**Wrong**

```c
struct A x; x.y = 10;   // x not defined
```

**Scenario:** Records, data aggregation.

---

### `union`

**Definition:** All members share the same memory location.

**Correct**

```c
union U { int x; float y; };
```

**Wrong**

```c
union U { int x; float y; } u;
u.x = 5; u.y = 3.2;   // logical misuse
```

**Scenario:** Memory-efficient variant storage.

---

### `enum`

**Definition:** Defines named integer constants.

**Correct**

```c
enum Day { MON, TUE };
```

**Wrong**

```c
enum Day { MON = "Monday" };
```

**Scenario:** Finite state representation.

---

## STORAGE CLASS SPECIFIERS

### `auto`

**Definition:** Automatic storage duration (default for locals).

**Correct**

```c
auto int x = 10;
```

**Wrong**

```c
auto x = 10;   // C requires explicit type
```

**Scenario:** Historical completeness.

---

### `register`

**Definition:** Suggests storage in CPU register.

**Correct**

```c
register int i;
```

**Wrong**

```c
register int *p; p = &i;   // address not allowed
```

**Scenario:** Performance hint.

---

### `static`

**Definition:** Preserves value or limits linkage.

**Correct**

```c
static int count;
```

**Wrong**

```c
static extern int x;   // contradictory
```

**Scenario:** Lifetime control, encapsulation.

---

### `extern`

**Definition:** Declares object defined elsewhere.

**Correct**

```c
extern int x;
```

**Wrong**

```c
extern int x = 10;   // definition, not declaration
```

**Scenario:** Multi-file programs.

---

### `_Thread_local`

**Definition:** Each thread has its own instance.

**Correct**

```c
_Thread_local int t;
```

**Wrong**

```c
_Thread_local static extern int t;
```

**Scenario:** Thread-specific data.

---

## TYPE QUALIFIERS

### `const`

**Definition:** Prevents modification through identifier.

**Correct**

```c
const int x = 5;
```

**Wrong**

```c
x = 10;
```

**Scenario:** Read-only safety.

---

### `volatile`

**Definition:** Prevents optimization on variable access.

**Correct**

```c
volatile int flag;
```

**Wrong**

```c
volatile int x = "A";
```

**Scenario:** Hardware or signal interaction.

---

### `restrict`

**Definition:** Pointer is sole reference to object.

**Correct**

```c
int *restrict p;
```

**Wrong**

```c
int *restrict p, *q = p;
```

**Scenario:** Optimization guarantee.

---

### `_Atomic`

**Definition:** Ensures atomic access.

**Correct**

```c
_Atomic int x;
```

**Wrong**

```c
_Atomic int x = x + 1;   // non-atomic expression
```

**Scenario:** Concurrency safety.

---

## CONTROL FLOW — SELECTION

### `if`

**Definition:** Executes block if condition true.

**Correct**

```c
if (x > 0) { }
```

**Wrong**

```c
if x > 0 { }
```

**Scenario:** Conditional execution.

---

### `else`

**Definition:** Executes when `if` is false.

**Correct**

```c
if (x) {} else {}
```

**Wrong**

```c
else { }   // without if
```

**Scenario:** Alternative path.

---

### `switch`

**Definition:** Multi-branch selection.

**Correct**

```c
switch(x) { case 1: break; }
```

**Wrong**

```c
switch(x) { case 1.5: ; }
```

**Scenario:** Menu/state logic.

---

### `case`

**Definition:** Labeled constant branch.

**Correct**

```c
case 2: break;
```

**Wrong**

```c
case x: ;   // must be constant
```

**Scenario:** Branch selection.

---

### `default`

**Definition:** Executes if no case matches.

**Correct**

```c
default: break;
```

**Wrong**

```c
default x: ;
```

**Scenario:** Fallback logic.

---

## CONTROL FLOW — LOOPS

### `for`

**Definition:** Loop with initialization, condition, update.

**Correct**

```c
for(int i=0;i<5;i++){}
```

**Wrong**

```c
for(i<5;i++){}
```

**Scenario:** Count-controlled loops.

---

### `while`

**Definition:** Loop with pre-condition check.

**Correct**

```c
while(x>0){}
```

**Wrong**

```c
while(x=5){}
```

**Scenario:** Condition-controlled loops.

---

### `do`

**Definition:** Loop executes at least once.

**Correct**

```c
do {} while(x);
```

**Wrong**

```c
do {} while;
```

**Scenario:** Mandatory first execution.

---

## CONTROL FLOW — JUMPS

### `break`

**Definition:** Exits loop or switch.

**Correct**

```c
break;
```

**Wrong**

```c
break x;
```

**Scenario:** Early termination.

---

### `continue`

**Definition:** Skips to next iteration.

**Correct**

```c
continue;
```

**Wrong**

```c
continue 2;
```

**Scenario:** Skip logic.

---

### `goto`

**Definition:** Unconditional jump.

**Correct**

```c
goto label;
label:;
```

**Wrong**

```c
goto 10;
```

**Scenario:** Low-level flow control.

---

### `return`

**Definition:** Ends function and returns value.

**Correct**

```c
return 0;
```

**Wrong**

```c
return x, y;
```

**Scenario:** Function result.

---

## FUNCTION / COMPILE-TIME

### `inline`

**Definition:** Suggests inline expansion.

**Correct**

```c
inline int f(){return 1;}
```

**Wrong**

```c
inline int x;
```

**Scenario:** Performance hint.

---

### `_Noreturn`

**Definition:** Function never returns.

**Correct**

```c
_Noreturn void exit_fn();
```

**Wrong**

```c
_Noreturn int f(){ return 1; }
```

**Scenario:** Program termination.

---

### `_Alignas`

**Definition:** Specifies alignment.

**Correct**

```c
_Alignas(16) int x;
```

**Wrong**

```c
_Alignas(x) int y;
```

**Scenario:** Memory alignment.

---

### `_Alignof`

**Definition:** Returns alignment requirement.

**Correct**

```c
_Alignof(int);
```

**Wrong**

```c
_Alignof(x);
```

**Scenario:** Layout queries.

---

### `_Generic`

**Definition:** Compile-time type selection.

**Correct**

```c
_Generic(x, int: 1, float: 2);
```

**Wrong**

```c
_Generic(x);
```

**Scenario:** Type-based dispatch.

---

### `_Static_assert`

**Definition:** Compile-time assertion.

**Correct**

```c
_Static_assert(sizeof(int)==4,"");
```

**Wrong**

```c
_Static_assert(x>0,"");
```

**Scenario:** Compile-time safety.

---

### `typedef`

**Definition:** Creates type alias.

**Correct**

```c
typedef int myint;
```

**Wrong**

```c
typedef int = myint;
```

**Scenario:** Readability, abstraction.
