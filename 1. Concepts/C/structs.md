# Structs

## Core Idea
Structs group heterogeneous data into one model.

## Why it exists
They represent domain entities clearly and reduce parameter clutter.

## Mental Model
Struct = custom record type with named fields.

## Code Pattern
~~~c
typedef struct {
    int id;
    char name[32];
} Student;
~~~

## Common Mistakes
- Uninitialized fields
- Passing huge structs by value unintentionally

## Interview Angle
- Padding and alignment basics
- struct pointer access (`->`)

## Related
- [[pointers]]
- [[memory_management]]
- [[functions]]

## Legacy Notes (archived)
# structs

Merged from legacy micro-notes.

## 11 10 typedef keyword

### 11.10 Typedef keyword
- Creates aliases for existing types
- Simplifies structure syntax
- Enhances code readability
- Facilitates portability across systems

## 11 2 structure declaration

### 11.2 Structure Declaration
- Use `struct` keyword
- Optional tag name
- Member declarations in braces `{}`
- End with semicolon `;`

## 11 3 accessing structure elements

### 11.3 Accessing Structure Elements
- Dot operator: `structure.member`
- Nested access: `outer.inner.member`
- Direct member access

## 11 4 structure memory allocation 2

### 11.4 Structure Memory Allocation
- Contiguous memory spaces
- Compiler may add padding for alignment
- Use `sizeof` to get actual size (padding included)
- Members stored in declaration order

## 11 5 structure initialization

### 11.5 Structure Initialization
- Direct: `struct Student s1 = {1, "Alice", 85.5};`
- Designated (C99): `struct Student s2 = {.rollno=2, .name="Bob", .marks=90.2};`
- Zero: `struct Student s3 = {0};`
- Copy: `struct Student s4 = s1;`

## 11 6 array of structures 2

### 11.6 Array of Structures
- Array where each element is a structure
- Store multiple records of same type
- Access: `array[index].member`
- Useful for database-like data

## 11 7 structure pointers 2

### 11.7 Structure Pointers
- Pointers that point to structure variables
- Same pointer arithmetic as structure arrays
- Access members via pointer

## 11 8 arrow operator 2

### 11.8 Arrow -> Operator
- Access structure me


## Questions
- When should I use this instead of an alternative?
- What edge case is most likely to break this approach?

