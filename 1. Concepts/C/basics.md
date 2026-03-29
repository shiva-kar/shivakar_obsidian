# basics

Merged from legacy micro-notes.

## 1 1 basic program structure 2

### 1.1 Basic Program Structure
```c
#include <stdio.h>

int main() {
    // say Hello to the world
    printf("Hello, World");
    return 0;
}
```

## 1 2 showing output 2

### 1.2 Showing Output
- The printf function is used for output
- Syntax: `printf("format string", variable1, variable2, ...);`
- Displaying Text: `printf("Hello, World!");`
- New Line: Use `\n` within the string
- Format Specifiers:
  - `%d` or `%i`: for integers
  - `%c`: for characters
  - `%f`: for decimal numbers

## 1 3 importance of the main method

### 1.3 Importance of the main Method
- Entry Point: Execution starts from main function
- Required: Every executable C program must have main function
- Return Type: Typically returns int (0 for success, non-zero for error)
- Fixed Name: Recognized by compilers as starting point

## 1 4 file extension

### 1.4 File Extension
- **.c**: Contains executable code, compiled into programs, hosts main function
- **.h**: Contains declarations, improves modularity, facilitates code sharing

## 1 5 comments

### 1.5 Comments
1. Used to add notes in C code
2. Not considered as part of code
3. Helpful for code organization
4. Syntax:
   - Single Line: `//`
   - Multi Line: `/* */`

## 1 6 coding using command line

### 1.6 Coding using Command Line
**Coding:**
- Write code using text editor
- Save file with .c extension

**Compiling and Running:**
- Use `gcc file -o outputname` to compile
- Run output file:
  - Windows: `.\outputname`
  - macOS/Linux: `./outputname`

## 1 7 what is a programming language

### 1.7 What is a Programming Language
- Giving instructions to a computer
- Instructions tell computer what to do
- Human instructions in high-level languages
- Compiler converts to machine code

## 1 9 what is syntax

### 1.9 What is Syntax
- Structure of words in a sentence
- Rules of the language
- Exact syntax must be followed in programming

## 1 first c program

## 1. First C Program

## 2 1 memory allocation 2

### 2.1 Memory Allocation
- Memory cells/locations have addresses
- Variables stored at specific memory addresses
- Each variable has name, address, and value

## 2 1 what are variables

### 2.1 What are Variables?
- Containers used for storing data values
- Variable Name → Variable Value

## 2 2 data types 2

### 2.2 Data Types
**Basic Data Types:**
- `char`: 1 byte, -128 to 127
- `short`: 2 bytes, -32,768 to 32,767
- `int`: 4 bytes, -2,147,483,648 to 2,147,483,647
- `long`: 4/8 bytes (system dependent)
- `float`: 4 bytes, ±3.4e±38
- `double`: 8 bytes, ±1.7e±308

**C Data Types Hierarchy:**
- Fundamental: void, char, int, float, double
- Derived: arrays, functions, pointers
- User-defined: structures, unions, enums, typedef

## 2 3 c identifier rules

### 2.3 C Identifier Rules
1. Only alphanumeric characters and underscore allowed
2. Cannot use keywords or reserved words
3. Cannot start with digits
4. Case-sensitive
5. No length limit, but 4-15 letters recommended

## 2 7 escape sequences

### 2.7 Escape Sequences
- `\t`: Insert tab
- `\b`: Insert backspace
- `\n`: Insert newline
- `\'`: Insert single quote
- `\"`: Insert double quote
- `\\`: Insert backslash

## 2 8 user input using scanf 2

### 2.8 User Input using scanf
1. Used for reading formatted input
2. Syntax: `scanf("format specifier", &variable);`
3. Format specifiers: `%d`, `%f`, `%c`, `%s`
4. Address operator `&` required (except arrays/strings)

## 2 9 sum of two numbers 2

### 2.9 Sum of Two Numbers
```c
#include <stdio.h>

int main() {
    int num1, num2, sum;
    
    printf("Enter first number: ");
    scanf("%d", &num1);
    
    printf("Enter second number: ");
    scanf("%d", &num2);
    
    sum = num1 + num2;
    
    printf("The sum of %d and %d is: %d\n", num1, num2, sum);
    return 0;
}
```

## 8 3 what are storage classes 2

### 8.3 What are Storage Classes
1. **Lifetime Management**: Determine variable scope and duration
2. **Scope Control**: Dictate variable accessibility
3. **Memory Location**: Influence storage location (stack, heap, data segment)
4. **Initialization**: Define default initial values

## 8 5 register 2

### 8.5 Register
- Hints compiler to store in CPU register for faster access
- Limited to variables that fit in registers
- No memory address (can't use `&`)
- Local to function/block
- For heavily used variables like loop counters

## 8 6 static

### 8.6 Static
- Retains value between function calls
- Automatically initialized to zero if no initial value
- Can be local to function or have file scope
- File-scope: visible only within declaring file
- Single instance, not recreated each call

## 8 7 external extern 2

### 8.7 External (extern)
- Defined in another file or outside functions
- Shared across multiple files
- Declaration references memory location without allocation
- Typically not initialized with declaration
- Useful for global variables accessed by multiple functions

## 8 8 usage of storage classes

### 8.8 Usage of Storage Classes
1. **auto**: Default for local variables, limited block scope/lifetime
2. **register**: Heavily used variables, compiler may ignore hint
3. **static**: Retain value between calls, limit file visibility
4. **extern**: Access variables across files, shared data

## 8 data types and storage classes

## 8. Data Types and Storage Classes

