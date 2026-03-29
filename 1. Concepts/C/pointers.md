# Pointers

## Core Idea
Pointers store addresses and enable direct memory control.

## Why it exists
Needed for dynamic memory, arrays, linked structures, and APIs.

## Mental Model
Pointer = address label; dereference = go to that address and read/write.

## Code Pattern
~~~c
int x = 10;
int *p = &x;
printf("%d\\n", *p);
~~~

## Common Mistakes
- Uninitialized pointer dereference
- Double free / use-after-free

## Interview Angle
- Pointer arithmetic
- Arrays vs pointers differences

## Related
- [[memory_management]]
- [[arrays]]
- [[structs]]

## Legacy Notes (archived)
# pointers

Merged from legacy micro-notes.

## 7 1 introduction to pointers 2

### 7.1 Introduction to Pointers
- Store memory addresses of other variables
- Rather than storing data itself
- Powerful feature for memory manipulation

## 7 2 address operator 2

### 7.2 & (Address) Operator
- Ampersand `&` gets variable's address
- Returns memory location where variable stored

## 7 3 value at address operator

### 7.3 * (Value at address) Operator
- Asterisk `*` gets value from particular address
- Called "value at address" or "dereference" operator

## 7 4 pointer declaration 2

### 7.4 Pointer Declaration
- Declared with asterisk before variable name
- Example: `int *ptr;`
- Stores memory addresses

## 7 5 pointer to a pointer 2

### 7.5 Pointer to a Pointer
- Pointer that stores address of another pointer
- Allows indirect access to variable value
- Multiple levels of indirection possible

## 7 6 call by reference 2

### 7.6 Call By Reference
1. Passes address of variables
2. Functions can modify actual values
3. Implemented using pointers
4. Avoids copying large data structures
5. Can return multiple values via out-parameters
6. Risk of unintended side effects

## 7 pointers 2

## 7. Pointers

## 7 pointers references

## 7. Pointers & References

- Raw pointers: declaration, `new`/`delete` (prefer smart pointers)
    
- Pointer to pointer
    
- References: `int &r = x;` (cannot be null, must be initialized)
    
- `nullptr` vs `NULL`
    
- `std::addressof`, `std::exchange` basics
    

```cpp
int x =


## Questions
- When should I use this instead of an alternative?
- What edge case is most likely to break this approach?

