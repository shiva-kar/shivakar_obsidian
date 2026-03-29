# Basics

## Core Idea
Build correct syntax, types, and program structure to express logic clearly.

## Why it exists
Without language basics, debugging and scaling become random.

## Mental Model
Basics are grammar + primitives + disciplined structure.

## Code Pattern
~~~c
#include <stdio.h>
int main(void) {
    int x = 0;
    printf("%d\\n", x);
    return 0;
}
~~~

## Common Mistakes
- Assuming compiler warnings can be ignored
- Mixing types carelessly

## Interview Angle
- Explain compilation stages briefly
- int vs float vs char tradeoffs

## Related
- [[operators]]
- [[control_flow]]
- [[functions]]

## Legacy Notes (archived)
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
  - Windows: `.\o
