# advanced topics

Consolidated from additional C notes to reduce file fragmentation.

## 1 10 what is a compiler

### 1.10 What is a Compiler
- **Pre-processing**: Processes directives like ``` 
  #include, #define ```
- **Compiling**: Transforms source code to assembly language
- **Assembling**: Converts assembly to machine code
- **Linking**: Combines object files into executable

## 11 1 why use structure

### 11.1 Why use Structure
1. Group related data items of different types
2. Model real-world entities naturally
3. Simplify passing multiple data as single argument
4. Enhance code readability and maintainability
5. Create new data types for specific needs

## 13 10 appending data to a file

### 13.10 Appending data to a File
- Open file in append mode (`"a"` or `"a+"`)
- New data added to end of file
- Existing content preserved
- File position set to end for writing

## 13 2 file operations

### 13.2 File Operations
1. **Creation**: Establish new file on disk
2. **Opening**: Acquire access to existing file
3. **Reading**: Retrieve data from file
4. **Writing**: Output data to file
5. **Seeking**: Move to specific file location
6. **Closing**: Release file and resources

## 14 1 what are preprocessor directives

### 14.1 What are Preprocessor Directives
- Processed before compilation
- Begin with `#` symbol
- Text substitution and file inclusion
- No semicolon required

## 14 preprocessor directives

## 14. Preprocessor Directives

## 14 preprocessor macros

## 14. Preprocessor & Macros

- `#include`, `#define`, conditional compilation (`#ifdef`) still present
    
- Prefer `constexpr`, `inline` functions and `enum class` over macros
    
- `static_assert` for compile-time checks

## 16 bitwise operations

## 16. Bitwise Operations

- Same operators as C
    
- Use `std::bitset` for safer bit manipulation
    
- Examples: masking, shifting, flags using `enum class` with bit operations

## 2 3 naming conventions

### 2.3 Naming Conventions
- **camelCase**: `myVariableName`
- **snake_case**: `my_variable_name`
- **kebab-case**: `my-variable-name`
- Keep descriptive but short names: `age`, `first_name`, `is_married`

## 24 1 header files math utils h

### 24.1 Header Files (math_utils.h)
```c
#ifndef MATH_UTILS_H
#define MATH_UTILS_H

// Function declarations
int add(int a, int b);
int subtract(int a, int b);
int multiply(int a, int b);
double divide(int a, int b);

// Constant definitions
#define PI 3.14159
#define MAX_VALUE 100

// Inline function
static inline int square(int x) {
    return x * x;
}

#endif
```

## 3 11 control instructions

### 3.11 Control Instructions
1. **Sequence**: Execute in written order
2. **Selection**: Choose instructions based on conditions (`if-else`)
3. **Loop**: Repeat instructions (`for`, `while`)
4. **Case**: Execute from multiple options (`switch`)

## 3 3 arithmetic operators

### 3.3 Arithmetic Operators
- `+`: Addition
- `-`: Subtraction
- `*`: Multiplication
- `/`: Division
- `%`: Modulus (remainder)

## 3 7 hierarchy of operations

### 3.7 Hierarchy of Operations
**Priority Order:**
1. `()`: Brackets
2. `*`, `/`, `%`: Multiplication, division, modulus
3. `+`, `-`: Addition, subtraction
4. `=`: Assignment

## 3 9 shorthand operators

### 3.9 Shorthand Operators
- `+=`: Addition assignment
- `-=`: Subtraction assignment
- `*=`: Multiplication assignment
- `/=`: Division assignment
- `%=`: Remainder assignment

## 4 10 switch

### 4.10 Switch
- Cleaner multi-way branching than multiple if-else
- Expression must be integer or character
- `case` labels represent branches
- `break` prevents fall-through
- `default` case for no matches

## 46 1 manipulators

### 46.1 Manipulators

```cpp
#include <iomanip>
std::cout << std::setw(10) << std::setfill('0') << 42;
```

## 5 1 need of loops

### 5.1 Need of Loops
1. Code runs multiple times based on condition
2. Repeated execution automation
3. Automates repetitive tasks
4. Types: `while`, `for`, `do-while`
5. Iterations: Number of loop executions

## 5 5 continue statement

### 5.5 Continue Statement
- Skips current iteration
- Starts next iteration immediately
- In while loop, increment manually before continue
- Helps avoid nested conditions

## 6 1 what is a function

### 6.1 What is a Function?
1. Blocks of reusable code
2. DRY Principle: "Don't Repeat Yourself"
3. Organizes code and performs tasks
4. Naming rules: snake_case
5. Example: Modular code components

## 6 6 passing values

### 6.6 Passing Values
1. Input values function takes
2. Parameters put values in, return gets values out
3. Multiple parameters possible
4. Same naming conventions as variables

## 64 1 compilation stages

### 64.1 Compilation Stages

1. Preprocessing
    
2. Compilation
    
3. Assembly
    
4. Linking

## 64 linking compilation and build pipelines

## 64. Linking, Compilation, and Build Pipelines

## 71 2 solid principles

### 71.2 SOLID Principles

1. **Single Responsibility**
    
2. **Open/Closed**
    
3. **Liskov Substitution**
    
4. **Interface Segregation**
    
5. **Dependency Inversion**

## 74 3 portability guidelines

### 74.3 Portability Guidelines

- Avoid platform APIs directly.
    
- Use `std::filesystem`, `std::thread`, `std::chrono` instead of OS calls.
    
- Test on multiple compilers.
    

---

## 8 2 signed and unsigned

### 8.2 Signed and Unsigned
- **Signed int**: Positive and negative numbers including zero
- **Unsigned int**: Only non-negative numbers (doubles positive range)
- **Range**: Signed: -2³¹ to 2³¹-1, Unsigned: 0 to 2³²-1 (32-bit)
- **Overflow**: Unsigned wraps around
- **Usage**: Unsigned for countable quantities

## advanced makefile example

# Advanced Makefile example
CC = gcc
CFLAGS = -Wall -Wextra -std=c11 -O2 -g
LDFLAGS = -lm -lpthread

## automatic dependency generation

# Automatic dependency generation
DEPFLAGS = -MT $@ -MMD -MP -MF $(OBJ_DIR)/$*.d

## basic const usage

###  **Basic const Usage**

#### const with Different Types
```c
#include <stdio.h>

int main() {
    // const variables
    const int MAX_SIZE = 100;
    // MAX_SIZE = 200;  // Error: cannot modify const
    
    // const with pointers
    int value = 10;
    const int *ptr1 = &value;  // Pointer to constant integer
    // *ptr1 = 20;  // Error: cannot modify through ptr1
    
    int *const ptr2 = &value;  // Constant pointer to integer
    *ptr2 = 20;  // OK: can modify value
    // ptr2 = NULL;  // Error: cannot change pointer
    
    // const with arrays
    const int numbers[] = {1, 2, 3, 4, 5};
    // numbers[0] = 10;  // Error: cannot modify const array
    
    return 0;
}
```

## basic goto usage

### **Basic goto Usage**

####  goto for Error Handling
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    FILE *file1 = NULL, *file2 = NULL;
    
    file1 = fopen("file1.txt", "r");
    if (file1 == NULL) {
        goto cleanup;
    }
    
    file2 = fopen("file2.txt", "w");
    if (file2 == NULL) {
        goto cleanup;
    }
    
    // Process files...
    printf("Files opened successfully\n");
    
cleanup:
    if (file1) fclose(file1);
    if (file2) fclose(file2);
    
    return 0;
}
```

## basic memory functions 2

###  **Basic Memory Functions**

#### Memory Manipulation
```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main() {
    int arr1[5] = {1, 2, 3, 4, 5};
    int arr2[5];
    
    // Memory copy
    memcpy(arr2, arr1, sizeof(arr1));
    printf("After memcpy: ");
    for (int i = 0; i < 5; i++) {
        printf("%d ", arr2[i]);
    }
    printf("\n");
    
    // Memory set
    int arr3[5];
    memset(arr3, 0, sizeof(arr3));  // Set all to zero
    printf("After memset: ");
    for (int i = 0; i < 5; i++) {
        printf("%d ", arr3[i]);
    }
    printf("\n");
    
    // Memory compare
    if (memcmp(arr1, arr2, sizeof(arr1)) == 0) {
        printf("Arrays are identical\n");
    } else {
        printf("Arrays are different\n");
    }
    
    return 0;
}
```

## basic variable arguments 2

###  **Basic Variable Arguments**

#### Simple Variable Arguments
```c
#include <stdio.h>
#include <stdarg.h>

// Simple variable argument function
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

int main() {
    printf("Sum of 3 numbers: %d\n", sum(3, 10, 20, 30));
    printf("Sum of 5 numbers: %d\n", sum(5, 1, 2, 3, 4, 5));
    
    return 0;
}
```

## basic volatile usage 2

### **Basic volatile Usage**

#### volatile Variables
```c
#include <stdio.h>
#include <signal.h>
#include <unistd.h>

volatile int flag = 0;

void handle_signal(int sig) {
    flag = 1;
}

int main() {
    signal(SIGINT, handle_signal);
    
    printf("Press Ctrl+C to set flag...\n");
    
    while (!flag) {
        // Without volatile, compiler might optimize this loop
        // With volatile, compiler always reads from memory
    }
    
    printf("Flag set! Exiting...\n");
    return 0;
}
```

## clean

# Clean
clean:
	rm -rf $(OBJ_DIR) $(BIN_DIR)

## create directories

# Create directories
$(BIN_DIR) $(OBJ_DIR):
	mkdir -p $@

## definition

### 6.3 Function Syntax / Definition
- Follows variable naming rules
- Uses `()` for parameters
- Fundamental for code organization and reusability
- Contains function header and body

## exercises mon sat full body 2

# **MON – Back + Biceps**

1. Lat Pulldown
2. Barbell Row
3. Chest-Supported Row (Machine)
4. Face Pull (Cable)
5. Barbell Curl
6. Incline Dumbbell Curl

---

# **TUE – Chest + Triceps**

1. Barbell Bench Press
2. Incline Dumbbell Press
3. Machine Chest Press
4. Pec Deck Fly
5. Cable Triceps Pushdown
6. Overhead Cable Triceps Extension

   ---

# **WED – Legs (Heavy)**

1. Barbell Back Squat
2. Romanian Deadlift
3. Leg Press
4. Seated Leg Curl
5. Walking Lunges
6. Standing Calf Raise

---

# **THU – Shoulders (Lateral + Rear) + Abs**

1. Dumbbell Shoulder Press
2. Cable Lateral Raise
3. Reverse Pec Deck
4. Face Pull
5. Cable Crunch
6. Hanging Leg Raise

---

# **FRI – Chest + Back (Compound Focus, No Arms)**

1. Barbell Bench Press (Heavy)
2. Pull-Ups
3. Barbell Row
4. Incline Machine Press
5. Chest-Supported Row
6. Dumbbell Chest Fly

---

# **SAT – Legs (Light) + Arms (Short)**

1. Bulgarian Split Squat
2. Hip Thrust
3. Leg Extension
4. Lying Leg Curl
5. Dumbbell Curl
6. Rope Triceps Pushdown

---

## exercism org 2

 https://exercism.org/tracks/c/exercises
# Full Exercise Sequence (1–84)

### Stage 1 — Core Control Flow

(loops, conditions, arithmetic)

1. [ ] Difference of Squares 
2. [ ] Grains
3. [ ] Collatz Conjecture
4. [ ] Darts
5. [ ] Triangle
6. [ ] Gigasecond
7. [ ] Leap *(redo if needed)*
8. [ ] Raindrops *(redo if needed)*
9. [ ] Armstrong Numbers *(redo if needed)*

---

### Stage 2 — Basic String Handling

(C strings, loops over arrays)

10. [ ] Reverse String *(redo)*
11. [ ] Pangram
12. [ ] Isogram
13. [ ] Acronym
14. [ ] Scrabble Score
15. [ ] RNA Transcription
16. [ ] Rotational Cipher
17. [ ] Atbash Cipher
18. [ ] Pig Latin

---

### Stage 3 — Bitwise and Binary Thinking

(bit operations, representation)

19. [ ] Binary
20. [ ] Eliud's Eggs
21. [ ] Secret Handshake
22. [ ] Allergies
23. [ ] Luhn

---

### Stage 4 — Numerical Algorithms

(more logic, nested loops)

24. [ ] Perfect Numbers
25. [ ] Sum of Multiples
26. [ ] Prime Factors
27. [ ] Nth Prime
28. [ ] Square Root
29. [ ] Pythagorean Triplet
30. [ ] Pascal's Triangle

---

### Stage 5 — String Parsing and Text Problems

(input processing and validation)

31. [ ] Hamming
32. [ ] Word Count
33. [ ] Phone Number
34. [ ] Matching Brackets
35. [ ] Series
36. [ ] Largest Series Product
37. [ ] Anagram
38. [ ] Bob
39. [ ] Wordy

---

### Stage 6 — Matrix / Grid Problems

(index reasoning)

40. [ ] Spiral Matrix
41. [ ] Saddle Points
42. [ ] Flower Field
43. [ ] Darts *(revisit for improvement)*

---

### Stage 7 — Encoding / Data Transformation

(data manipulation)

44. [ ] Run-Length Encoding
45. [ ] Rail Fence Cipher
46. [ ] Crypto Square
47. [ ] ETL
48. [ ] Roman Numerals
49. [ ] Say

---

### Stage 8 — Base Systems / Representation

(number systems)

50. [ ] All Your Base
51. [ ] Variable Length Quantity
52. [ ] Binary *(revisit advanced implementation)*

 ---

### Stage 9 — Simulation Problems

(state machines and logic)

53. [ ] Robot Simulator
54. [ ] Clock
55. [ ] Meetup
56. [ ] Beer Song
57. [ ] Kindergarten Garden

---

### Stage 10 — Object-like Struct Design

(structs, data modeling)

58. [ ] High Scores
59. [ ] Grade School
60. [ ] D&D Character
61. [ ] Rational Numbers
62. [ ] Complex Numbers

---

### Stage 11 — Array / List Operations

(introducing list logic)

63. [ ] Sublist
64. [ ] List Ops

---

 ### Stage 12 — True Data Structures

(real DSA work)

65. [ ] Linked List
66. [ ] Circular Buffer
67. [ ] Binary Search
68. [ ] Binary Search Tree

 ---

### Stage 13 — Advanced Logical Problems

69. [ ] Two Bucket
70. [ ] Yacht
71. [ ] Intergalactic Transmission
72. [ ] Zebra Puzzle

---

### Stage 14 — Pattern / Output Problems

73. [ ] Diamond

 ---

### Stage 15 — Cryptography / Encoding Advanced

74. [ ] Rotational Cipher *(revisit optimized)*
75. [ ] Atbash Cipher *(revisit optimized)*

 ---

### Stage 16 — Heavy Algorithm Problems

76. [ ] Knapsack
77. [ ] Palindrome Products

 ---

### Stage 17 — Reactive / Systems-style Problems

78. [ ] React

---

### Stage 18 — Final Algorithm Challenges

79. [ ] Spiral Matrix *(revisit optimized)*
80. [ ] Matching Brackets *(revisit optimized)*
81. [ ] Run-Length Encoding *(revisit optimized)*
82. [ ] Word Count *(revisit optimized)*
83. [ ] Binary Search Tree *(revisit optimized)*
84. [ ] Circular Buffer *(revisit optimized)*

---

## include dependencies

# Include dependencies
-include $(DEPENDS)

## installation compiler setup

## Installation & Compiler Setup

## longjmp 2

### **Basic setjmp/longjmp**

####  Non-local Jumps
```c
#include <stdio.h>
#include <setjmp.h>
#include <stdlib.h>

jmp_buf env;

void function_b() {
    printf("In function_b\n");
    longjmp(env, 1);  // Jump back to setjmp point
    printf("This won't be printed\n");
}

void function_a() {
    printf("In function_a\n");
    function_b();
    printf("This won't be printed either\n");
}

int main() {
    if (setjmp(env) == 0) {
        printf("First time through\n");
        function_a();
    } else {
        printf("After longjmp\n");
    }
    
    return 0;
}
```

## main target

# Main target
$(TARGET): $(OBJECTS) | $(BIN_DIR)
	$(CC) $(OBJECTS) -o $@ $(LDFLAGS)

## mathematical functions 2

###  **Mathematical Functions**

####  math.h Basics
```c
#include <stdio.h>
#include <math.h>

int main() {
    double x = 2.5, y = 3.0;
    
    printf("sqrt(%.2f) = %.2f\n", x, sqrt(x));
    printf("pow(%.2f, %.2f) = %.2f\n", x, y, pow(x, y));
    printf("sin(%.2f) = %.2f\n", x, sin(x));
    printf("cos(%.2f) = %.2f\n", x, cos(x));
    printf("log(%.2f) = %.2f\n", x, log(x));
    printf("exp(%.2f) = %.2f\n", x, exp(x));
    printf("ceil(%.2f) = %.2f\n", x, ceil(x));
    printf("floor(%.2f) = %.2f\n", x, floor(x));
    printf("fabs(%.2f) = %.2f\n", -x, fabs(-x));
    
    return 0;
}
```

## most used basic topics

## ##. Most Used Basic Topics

## o 2

## 13. Files I/O

- `<fstream>`: `std::ifstream`, `std::ofstream`, `std::fstream`
    
- Binary vs text modes
    
- Use RAII to manage files (destructor closes file)

## object files

# Object files
$(OBJ_DIR)/%.o: $(SRC_DIR)/%.c | $(OBJ_DIR)
	$(CC) $(CFLAGS) $(DEPFLAGS) -c $< -o $@

## output 2

## 13. File Input/Output

## output advanced topics

## 46. Input/Output Advanced Topics

## output variations 2

### **Basic Input/Output Variations**

#### Character I/O
```c
#include <stdio.h>

int main() {
    char ch;
    
    printf("Enter a character: ");
    ch = getchar();  // Read single character
    printf("You entered: ");
    putchar(ch);     // Write single character
    putchar('\n');
    
    // Using getc and putc
    printf("Enter another character: ");
    ch = getc(stdin);
    printf("You entered: ");
    putc(ch, stdout);
    putc('\n', stdout);
    
    return 0;
}
```

####  String I/O
```c
#include <stdio.h>

int main() {
    char name[50];
    
    printf("Enter your name: ");
    fgets(name, sizeof(name), stdin);  // Safe string input
    
    printf("Hello, ");
    fputs(name, stdout);  // String output
    
    return 0;
}
```

## output

## 2. Variables, Data Types & Input/Output

## source directories

# Source directories
SRC_DIR = src
OBJ_DIR = obj
BIN_DIR = bin

## source files

# Source files
SOURCES = $(wildcard $(SRC_DIR)/*.c)
OBJECTS = $(SOURCES:$(SRC_DIR)/%.c=$(OBJ_DIR)/%.o)
DEPENDS = $(OBJECTS:.o=.d)

## storage duration concepts 2

###  **Storage Duration Concepts**

####  Automatic vs Static Duration
```c
#include <stdio.h>

void test_storage_duration() {
    int auto_var = 0;        // Automatic storage duration
    static int static_var = 0; // Static storage duration
    
    auto_var++;
    static_var++;
    
    printf("auto_var: %d, static_var: %d\n", auto_var, static_var);
}

int main() {
    printf("First call:\n");
    test_storage_duration();
    
    printf("Second call:\n");
    test_storage_duration();
    
    printf("Third call:\n");
    test_storage_duration();
    
    return 0;
}
```

## targets

# Targets
TARGET = $(BIN_DIR)/program

## type conversion rules 2

###  **Type Conversion Rules**

####  Implicit Type Conversion
```c
#include <stdio.h>

int main() {
    // Integer promotion
    char c1 = 100, c2 = 100;
    int result = c1 * c2;  // chars promoted to int
    printf("char * char = int: %d\n", result);
    
    // Usual arithmetic conversions
    int i = 10;
    float f = 3.14;
    double d = i + f;  // i converted to float, then to double
    printf("int + float = double: %.2f\n", d);
    
    // Sign extension
    signed char sc = -10;
    unsigned char uc = 200;
    int signed_extended = sc;    // Sign extended
    int unsigned_extended = uc;  // Zero extended
    printf("Signed char extended: %d\n", signed_extended);
    printf("Unsigned char extended: %d\n", unsigned_extended);
    
    return 0;
}
```

## type modifiers 2

###  **Type Modifiers**

####  signed and unsigned
```c
#include <stdio.h>
#include <limits.h>

int main() {
    signed int s_int = -100;
    unsigned int u_int = 100;
    
    printf("Signed int range: %d to %d\n", INT_MIN, INT_MAX);
    printf("Unsigned int range: 0 to %u\n", UINT_MAX);
    
    // Be careful with mixing signed and unsigned
    int signed_val = -5;
    unsigned int unsigned_val = 10;
    
    if (signed_val < unsigned_val) {
        printf("This might not work as expected!\n");
    }
    
    return 0;
}
```

####  short and long
```c
#include <stdio.h>

int main() {
    short small_number = 32767;  // Typically 2 bytes
    int normal_number = 2147483647;  // Typically 4 bytes
    long large_number = 2147483647L;  // Typically 4 or 8 bytes
    long long very_large = 9223372036854775807LL;  // Typically 8 bytes
    
    printf("short: %hd, size: %zu bytes\n", small_number, sizeof(short));
    printf("int: %d, size: %zu bytes\n", normal_number, sizeof(int));
    printf("long: %ld, size: %zu bytes\n", large_number, sizeof(long));
    printf("long long: %lld, size: %zu bytes\n", very_large, sizeof(long long));
    
    return 0;
}
```

## unique ptr example

### unique_ptr example

```cpp
#include <memory>
#include <iostream>

struct Node { int v; std::unique_ptr<Node> next; };

int main() {
    auto head = std::make_unique<Node>();
    head->v = 1;
    head->next = std::make_unique<Node>();
    head->next->v = 2;
}
```

## what is an ide

### What is an IDE?
1. IDE stands for Integrated Development Environment.
2. Software suite that consolidates basic tools required for software development.
3. Central hub for coding, finding problems, and testing.
4. Designed to improve developer efficiency.

