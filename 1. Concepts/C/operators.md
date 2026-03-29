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
- Example: `int a = 5;`

## 3 2 type declaration instruction

### 3.2 Type Declaration Instruction
1. Define variable and function data types
2. Syntax: `data_type variable_name;`
3. Common types: `int`, `float`, `char`, `double`
4. Allows immediate assignment: `int count = 10;`
5. Scope dictates variable visibility

## 3 4 arithmetic instruction

### 3.4 Arithmetic Instruction
- Variable on left of `=`
- Right side can have variables, operators, constants
- Types: Integer Mode, Real Mode, Mixed Mode

## 3 5 integer and float conversions

### 3.5 Integer and Float Conversions
1. Integer ÷ Integer = Integer
2. Real ÷ Real = Real
3. Integer ÷ Real = Real (integer promoted first)

## 3 6 type conversions

### 3.6 Type Conversions
1. **Implicit**: Automatic type changes when needed
2. **Promotion**: Smaller types promoted to int
3. **Assignment**: Type converted to match variable type
4. **Casting**: Explicit conversion using `(type_name)`

## 3 8 associativity of operations

### 3.8 Associativity of Operations
- **Operator Precedence**: Evaluation order based on priority
- **Associativity**: Order for same precedence operators
- Most operators: Left-to-right
- Assignment, unary: Right-to-left

## 3 expressions operators

## 3. Expressions & Operators

- Arithmetic, relational, logical, bitwise (same as C)
    
- Additional: scope resolution `::`, `.*` and `->*` (pointer-to-member).
    
- Overloadable operators (see Operator Overloading section).

## 3 instructions expressions operators

## 3. Instructions, Expressions & Operators

## operators in detail 2

### **Operators in Detail**
####  Comma Operator
```c
#include <stdio.h>

int main() {
    int a, b, c;
    
    // Comma operator example
    a = (b = 3, c = 4, b + c); // a gets 7
    printf("a = %d, b = %d, c = %d\n", a, b, c);
    
    // In for loops
    for (int i = 0, j = 10; i < j; i++, j--) {
        printf("i = %d, j = %d\n", i, j);
    }
    
    return 0;
}
```

####  sizeof Operator
```c
#include <stdio.h>

int main() {
    int arr[10];
    
    printf("Size of int: %zu bytes\n", sizeof(int));
    printf("Size of array: %zu bytes\n", sizeof(arr));
    printf("Number of elements: %zu\n", sizeof(arr) / sizeof(arr[0]));
    
    // sizeof with expressions
    int x = 5;
    printf("Size of expression: %zu\n", sizeof(x + 3.14));
    
    return 0;
}
```

#### Conditional Operator
```c
#include <stdio.h>

int main() {
    int a = 10, b = 20;
    
    // Basic conditional operator
    int max = (a > b) ? a : b;
    printf("Maximum: %d\n", max);
    
    // Nested conditional operator
    int num = -5;
    char* result = (num > 0) ? "Positive" : (num < 0) ? "Negative" : "Zero";
    printf("Number is: %s\n", result);
    
    return 0;
}
```

