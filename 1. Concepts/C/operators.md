# Operators

## Core Idea
Operators transform values and drive expression evaluation.

## Why it exists
They are the building blocks of conditions, math, and state updates.

## Mental Model
Think of operators as tiny functions with precedence and associativity rules.

## Code Pattern
~~~c
int a = 5, b = 2;
int sum = a + b;
int ok = (a > b) && (b != 0);
~~~

## Common Mistakes
- Wrong precedence assumptions
- Assignment `=` used instead of comparison `==`

## Interview Angle
- Operator precedence traps
- Bitwise vs logical operators

## Related
- [[control_flow]]
- [[pointers]]
- [[arrays]]

## Legacy Notes (archived)
# operators

Merged from legacy micro-notes.

## 16 1 bitwise operators

### 16.1 Bitwise Operators
- `&` : AND
- `|` : OR
- `^` : XOR
- `~` : NOT (One's complement)
- `<<` : Left shift
- `>>` : Right shift

## 16 2 practical examples 2

### 16.2 Practical Examples
```c
#include <stdio.h>

void printBinary(unsigned int num) {
    for (int i = 31; i >= 0; i--) {
        printf("%d", (num >> i) & 1);
        if (i % 8 == 0) printf(" ");
    }
    printf("\n");
}

int main() {
    unsigned int a = 5;    // 00000101
    unsigned int b = 3;    // 00000011
    
    printf("a & b  = "); printBinary(a & b);   // AND: 00000001 (1)
    printf("a | b  = "); printBinary(a | b);   // OR:  00000111 (7)
    printf("a ^ b  = "); printBinary(a ^ b);   // XOR: 00000110 (6)
    printf("~a     = "); printBinary(~a);      // NOT: 11111010 (large number)
    printf("a << 1 = "); printBinary(a << 1);  // Left shift: 00001010 (10)
    printf("a >> 1 = "); printBinary(a >> 1);  // Right shift: 00000010 (2)
    
    return 0;
}
```

## 16 bitwise operations

## 16. Bitwise Operations

## 3 1 c instructions

### 3.1 C Instructions
1. **Type Declaration**: Declare variable types
2. **Arithmetic**: Perform arithmetic operations
3. **Control**: Control execution sequence

## 3 10 unary operators

### 3.10 Unary Operators
- `-`: Negation
- `++`: Increment
- `--`: Decrement
- Types: Pre-increment/decrement, Post-increment/decrement

## 3 2 assignment operator

### 3.2 Assignment Operator
- `=`: Assigns right-hand value to left-hand operand


## Questions
- When should I use this instead of an alternative?
- What edge case is most likely to break this approach?

