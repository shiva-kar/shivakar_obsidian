# Functions

## Core Idea
Functions package logic into reusable units.

## Why it exists
They reduce duplication and improve testability.

## Mental Model
Each function should do one clear job with explicit inputs/outputs.

## Code Pattern
~~~c
int add(int a, int b) { return a + b; }
int main(void) { printf("%d\\n", add(2,3)); }
~~~

## Common Mistakes
- Hidden side effects via globals
- Mismatched prototypes and definitions

## Interview Angle
- Call by value in C
- Recursion base case design

## Related
- [[basics]]
- [[control_flow]]
- [[pointers]]

## Legacy Notes (archived)
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

### 21.1 Inline Functi


## Questions
- When should I use this instead of an alternative?
- What edge case is most likely to break this approach?

