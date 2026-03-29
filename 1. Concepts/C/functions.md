# functions

Merged from legacy micro-notes.

## 15 2 processing command line arguments 2

### 15.2 Processing Command Line Arguments
```c
#include <stdio.h>

int main(int argc, char *argv[]) {
    printf("Program name: %s\n", argv[0]);
    printf("Number of arguments: %d\n", argc - 1);
    
    for (int i = 1; i < argc; i++) {
        printf("Argument %d: %s\n", i, argv[i]);
    }
    return 0;
}
```

## 15 3 argument parsing example 2

### 15.3 Argument Parsing Example
```c
#include <stdio.h>
#include <stdlib.h>

int main(int argc, char *argv[]) {
    if (argc != 4) {
        printf("Usage: %s <operation> <num1> <num2>\n", argv[0]);
        return 1;
    }
    
    char operation = argv[1][0];
    int num1 = atoi(argv[2]);
    int num2 = atoi(argv[3]);
    int result;
    
    switch (operation) {
        case '+': result = num1 + num2; break;
        case '-': result = num1 - num2; break;
        case '*': result = num1 * num2; break;
        case '/': result = num1 / num2; break;
        default:
            printf("Invalid operation\n");
            return 1;
    }
    
    printf("Result: %d\n", result);
    return 0;
}
```

## 15 command line arguments 2

## 15. Command Line Arguments

- `int main(int argc, char *argv[])`
    
- Prefer `std::string_view`/`std::string` for argument parsing
    
- Use libraries for complex parsing (e.g., `getopt`, `args`, `Boost.Program_options`)

## 15 command line arguments

## 15. Command Line Arguments

## 21 1 inline function definition 2

### 21.1 Inline Function Definition
```c
#include <stdio.h>

// Inline function suggestion to compiler
static inline int max(int a, int b) {
    return (a > b) ? a : b;
}

static inline double square(double x) {
    return x * x;
}

int main() {
    int a = 10, b = 20;
    double x = 5.5;
    
    printf("Max of %d and %d: %d\n", a, b, max(a, b));
    printf("Square of %.2f: %.2f\n", x, square(x));
    
    return 0;
}
```

## 21 inline functions

## 21. Inline Functions

## 28 1 basic function pointers 2

### 28.1 Basic Function Pointers
```c
#include <stdio.h>

int add(int a, int b) {
    return a + b;
}

int subtract(int a, int b) {
    return a - b;
}

int multiply(int a, int b) {
    return a * b;
}

int divide(int a, int b) {
    return b != 0 ? a / b : 0;
}

int main() {
    // Function pointer declaration
    int (*operation)(int, int);
    
    int x = 10, y = 5;
    
    // Use function pointer
    operation = add;
    printf("%d + %d = %d\n", x, y, operation(x, y));
    
    operation = subtract;
    printf("%d - %d = %d\n", x, y, operation(x, y));
    
    operation = multiply;
    printf("%d * %d = %d\n", x, y, operation(x, y));
    
    operation = divide;
    printf("%d / %d = %d\n", x, y, operation(x, y));
    
    return 0;
}
```

## 28 2 function pointer arrays 2

### 28.2 Function Pointer Arrays
```c
#include <stdio.h>

void sayHello() {
    printf("Hello!\n");
}

void sayGoodbye() {
    printf("Goodbye!\n");
}

void sayThanks() {
    printf("Thank you!\n");
}

int main() {
    // Array of function pointers
    void (*functions[])() = {sayHello, sayGoodbye, sayThanks};
    
    int choice;
    
    printf("Choose an option (0=Hello, 1=Goodbye, 2=Thanks): ");
    scanf("%d", &choice);
    
    if (choice >= 0 && choice <= 2) {
        functions[choice]();
    } else {
        printf("Invalid choice\n");
    }
    
    return 0;
}
```

## 28 function pointers 2

## 28. Function Pointers

## 29 1 variable argument functions 2

### 29.1 Variable Argument Functions
```c
#include <stdio.h>
#include <stdarg.h>

// Simple variadic function
int sum(int count, ...) {
    va_list args;
    va_start(args, count);
    
    int total = 0;
    for (int i = 0; i < count; i++) {
        total += va_arg(args, int);
    }
    
    va_end(args);
    return total;
}

// Variadic function with format string
void printValues(const char *format, ...) {
    va_list args;
    va_start(args, format);
    
    while (*format) {
        switch (*format) {
            case 'd':
                printf("%d ", va_arg(args, int));
                break;
            case 'f':
                printf("%.2f ", va_arg(args, double));
                break;
            case 'c':
                printf("%c ", va_arg(args, int));  // char promoted to int
                break;
            case 's':
                printf("%s ", va_arg(args, char*));
                break;
        }
        format++;
    }
    printf("\n");
    
    va_end(args);
}

int main() {
    printf("Sum of 3 numbers: %d\n", sum(3, 10, 20, 30));
    printf("Sum of 5 numbers: %d\n", sum(5, 1, 2, 3, 4, 5));
    
    printValues("dfs", 42, 3.14159, "Hello");
    printValues("cccd", 'A', 'B', 'C', 100);
    
    return 0;
}
```

## 29 variadic functions

## 29. Variadic Functions

## 29 variadic templates parameter packs

## 29. Variadic Templates & Parameter Packs

- Implement `printf`-like functionality with type safety using variadic templates
    
- Example skeleton:
    

```cpp
template<typename... Args>
void log(Args&&... args) {
    (std::cout << ... << args) << '\n'; // fold expression (C++17)
}
```

## 6 10 recursion 2

### 6.10 Recursion
1. **Self-Calling**: Function calls itself
2. **Base Case**: Essential to stop recursion
3. **Recursive Case**: Condition for continued calling
4. **Stack Usage**: Consumes stack space, risk of overflow
5. **Applications**: Tree/graph traversals, sorting algorithms
6. **Memory Intensive**: More overhead than iterative solutions
7. **Clarity**: Simplifies complex problems

## 6 2 function prototype

### 6.2 Function Prototype
- Specifies name, return type, parameters without body
- Enables type checking and forward declaration
- Parameter names optional in prototypes
- Placed at file start or in header files

## 6 4 function call

### 6.4 Function Call
- Invoke using function name followed by `()`
- Executes function code
- Can pass arguments

## 6 5 return statement

### 6.5 Return Statement
1. Sends value back from function
2. Can return values, variables, calculations
3. Ends function immediately
4. Function calls make code jump around
5. Prefer returning values over global variables

## 6 7 argument vs parameter

### 6.7 Argument vs Parameter
- **Parameters**: Variables in function definition (placeholders)
- **Arguments**: Actual values passed at call time

## 6 8 call by value 2

### 6.8 Call by Value
1. Passes argument's copy, not original
2. Parameters use separate memory
3. Original data unchanged
4. Cannot modify original arguments directly
5. Good for small data types

## 6 9 scoping rule

### 6.9 Scoping Rule
1. **Local Scope**: Variables inside functions, not accessible outside
2. **Global Scope**: Variables outside functions, accessible anywhere in file
3. **Block Scope**: Variables in blocks accessible only within blocks
4. **Function Parameters**: Act as local variables
5. **Lifetime**: Local variables exist during function execution only

## 6 function and recursion

## 6. Function and Recursion

## 6 functions and recursion

## 6. Functions and Recursion

- Function declarations, default parameters, inline functions
    
- `constexpr` functions (evaluated at compile-time when possible)
    
- Function overloading
    
- `noexcept` specification
    
- Passing by value, by pointer, by reference, `const &` for efficiency
    

```cpp
int sum(int a, int b = 0) { return a + b; }
```

