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
- Access structure members through pointer
- Syntax: `pointer->member`
- Equivalent to `(*pointer).member`
- More concise than dereferencing
- Common in linked lists

## 11 9 structure as function arguments

### 11.9 Structure as Function Arguments
- **Direct passing**: Copies whole structure (less efficient)
- **Pass by address**: More efficient, allows modifications
- **Performance**: Address passing faster for large structures
- **Simplicity**: Direct passing simpler but less flexible

## 11 structs and classes oop

## 11. Structs and Classes (OOP)

- `struct` vs `class` (default public vs private)
    
- Access specifiers: `public`, `protected`, `private`
    
- Member functions, data members
    
- Constructors, destructors
    
- `this` pointer
    
- `friend` functions/classes
    
- Example:
    

```cpp
#include <string>
#include <iostream>

class Person {
public:
    Person(std::string n, int a): name(std::move(n)), age(a) {}
    void greet() const { std::cout << "Hi, I'm " << name << '\n'; }
private:
    std::string name;
    int age;
};
```

## 11 structures

## 11. Structures

## 17 1 what are unions 2

### 17.1 What are Unions
- Similar to structures but share memory
- All members share same memory location
- Size equals largest member size

## 17 2 union declaration and usage 2

### 17.2 Union Declaration and Usage
```c
#include <stdio.h>

union Data {
    int i;
    float f;
    char str[20];
};

int main() {
    union Data data;
    
    printf("Memory size occupied by data: %lu\n", sizeof(data));
    
    data.i = 10;
    printf("data.i: %d\n", data.i);
    
    data.f = 220.5;
    printf("data.f: %.2f\n", data.f);
    
    // data.i is now corrupted because memory is shared
    printf("data.i after setting f: %d (corrupted)\n", data.i);
    
    return 0;
}
```

## 17 3 practical use case variant type 2

### 17.3 Practical Use Case: Variant Type
```c
#include <stdio.h>

typedef enum { INT, FLOAT, CHAR } Type;

typedef struct {
    Type type;
    union {
        int i;
        float f;
        char c;
    } value;
} Variant;

void printVariant(Variant v) {
    switch (v.type) {
        case INT:
            printf("Integer: %d\n", v.value.i);
            break;
        case FLOAT:
            printf("Float: %.2f\n", v.value.f);
            break;
        case CHAR:
            printf("Char: %c\n", v.value.c);
            break;
    }
}

int main() {
    Variant v1 = {INT, {.i = 10}};
    Variant v2 = {FLOAT, {.f = 3.14}};
    Variant v3 = {CHAR, {.c = 'A'}};
    
    printVariant(v1);
    printVariant(v2);
    printVariant(v3);
    
    return 0;
}
```

## 17 unions

## 17. Unions

## 18 2 enum usage 2

### 18.2 Enum Usage
```c
#include <stdio.h>

enum TrafficLight { RED, YELLOW, GREEN };

const char* getLightColor(enum TrafficLight light) {
    switch (light) {
        case RED: return "Stop";
        case YELLOW: return "Caution";
        case GREEN: return "Go";
        default: return "Unknown";
    }
}

int main() {
    enum TrafficLight current = RED;
    
    printf("Current light: %s\n", getLightColor(current));
    
    // Iterate through enum values
    for (enum TrafficLight light = RED; light <= GREEN; light++) {
        printf("Light %d: %s\n", light, getLightColor(light));
    }
    
    return 0;
}
```

## 18 enumerations 2

## 18. Enumerations

- `enum class` (scoped enums) prefered over plain `enum`
    
- Typed enums: `enum class Color : uint8_t { Red, Green, Blue };`

## 18 enumerations

## 18. Enumerations

