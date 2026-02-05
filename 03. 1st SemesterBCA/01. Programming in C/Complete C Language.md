## Installation & Compiler Setup

### What is an IDE?
1. IDE stands for Integrated Development Environment.
2. Software suite that consolidates basic tools required for software development.
3. Central hub for coding, finding problems, and testing.
4. Designed to improve developer efficiency.

### Need for an IDE
1. Streamlines development.
2. Increases productivity.
3. Simplifies complex tasks.
4. Offers a unified workspace.
5. IDE Features:
    1. Code Autocomplete
    2. Syntax Highlighting
    3. Version Control
    4. Error Checking

### Windows Installation
- Search VS Code on Google
- Download and install Visual Studio Code
- Install C/C++ extensions
- Download and install MSYS2
- Install MinGW toolchain
- Add MinGW to system PATH
- Configure VS Code for C/C++ development

### Mac Installation
- Search VS Code on Google
- Download and install Visual Studio Code
- Install C/C++ extensions
- Ensure Clang is installed (comes with Xcode)
- Verify installation using `clang --version`
Looking at the basic topics covered, here are some important fundamental C programming topics that were missed or could use more detailed coverage:

## 1. First C Program

### 1.1 Basic Program Structure
```c
#include <stdio.h>

int main() {
    // say Hello to the world
    printf("Hello, World");
    return 0;
}
```

### 1.2 Showing Output
- The printf function is used for output
- Syntax: `printf("format string", variable1, variable2, ...);`
- Displaying Text: `printf("Hello, World!");`
- New Line: Use `\n` within the string
- Format Specifiers:
  - `%d` or `%i`: for integers
  - `%c`: for characters
  - `%f`: for decimal numbers

### 1.3 Importance of the main Method
- Entry Point: Execution starts from main function
- Required: Every executable C program must have main function
- Return Type: Typically returns int (0 for success, non-zero for error)
- Fixed Name: Recognized by compilers as starting point

### 1.4 File Extension
- **.c**: Contains executable code, compiled into programs, hosts main function
- **.h**: Contains declarations, improves modularity, facilitates code sharing

### 1.5 Comments
1. Used to add notes in C code
2. Not considered as part of code
3. Helpful for code organization
4. Syntax:
   - Single Line: `//`
   - Multi Line: `/* */`

### 1.6 Coding using Command Line
**Coding:**
- Write code using text editor
- Save file with .c extension

**Compiling and Running:**
- Use `gcc file -o outputname` to compile
- Run output file:
  - Windows: `.\outputname`
  - macOS/Linux: `./outputname`

### 1.7 What is a Programming Language
- Giving instructions to a computer
- Instructions tell computer what to do
- Human instructions in high-level languages
- Compiler converts to machine code

### 1.8 What is an Algorithm
- Step-by-step procedure for solving problems
- Examples: Making tea, using hand sanitizer

### 1.9 What is Syntax
- Structure of words in a sentence
- Rules of the language
- Exact syntax must be followed in programming

### 1.10 What is a Compiler
- **Pre-processing**: Processes directives like ``` 
  #include, #define ```
- **Compiling**: Transforms source code to assembly language
- **Assembling**: Converts assembly to machine code
- **Linking**: Combines object files into executable

## 2. Variables, Data Types & Input/Output

### 2.1 What are Variables?
- Containers used for storing data values
- Variable Name → Variable Value

### 2.1 Memory Allocation
- Memory cells/locations have addresses
- Variables stored at specific memory addresses
- Each variable has name, address, and value

### 2.1 Variable Declaration
```c
data_type variable_name = value;
int age = 20;
```
- Data type specifies what kind of data variable can hold
- Variable name identifies the variable
- Value is the actual data stored

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

### 2.3 Naming Conventions
- **camelCase**: `myVariableName`
- **snake_case**: `my_variable_name`
- **kebab-case**: `my-variable-name`
- Keep descriptive but short names: `age`, `first_name`, `is_married`

### 2.3 C Identifier Rules
1. Only alphanumeric characters and underscore allowed
2. Cannot use keywords or reserved words
3. Cannot start with digits
4. Case-sensitive
5. No length limit, but 4-15 letters recommended

### 2.4 Literals
- Fixed values directly written in code
- Examples: `0, 1, 2, 3`, `'A'`, `3.14`, `"Hello"`
- Types: integer, floating-point, character, string literals

### 2.5 Constants
1. Fixed values that don't change during execution
2. Defined using `#define` or `const`
3. Enhance code readability and ease modifications
4. Immutable
```c
#define PI 3.1425
const float PI = 3.1425;
```

### 2.6 Keywords
Reserved words in C:
```
auto        double      int         struct
break       else        long        switch
case        enum        register    typedef
char        extern      return      union
const       float       short       unsigned
continue    for         signed      void
default     goto        sizeof      volatile
do          if          static      while
```

### 2.7 Escape Sequences
- `\t`: Insert tab
- `\b`: Insert backspace
- `\n`: Insert newline
- `\'`: Insert single quote
- `\"`: Insert double quote
- `\\`: Insert backslash

### 2.8 User Input using scanf
1. Used for reading formatted input
2. Syntax: `scanf("format specifier", &variable);`
3. Format specifiers: `%d`, `%f`, `%c`, `%s`
4. Address operator `&` required (except arrays/strings)

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

## 3. Instructions, Expressions & Operators

### 3.1 C Instructions
1. **Type Declaration**: Declare variable types
2. **Arithmetic**: Perform arithmetic operations
3. **Control**: Control execution sequence

### 3.2 Assignment Operator
- `=`: Assigns right-hand value to left-hand operand
- Example: `int a = 5;`

### 3.2 Type Declaration Instruction
1. Define variable and function data types
2. Syntax: `data_type variable_name;`
3. Common types: `int`, `float`, `char`, `double`
4. Allows immediate assignment: `int count = 10;`
5. Scope dictates variable visibility

### 3.3 Arithmetic Operators
- `+`: Addition
- `-`: Subtraction
- `*`: Multiplication
- `/`: Division
- `%`: Modulus (remainder)

### 3.4 Arithmetic Instruction
- Variable on left of `=`
- Right side can have variables, operators, constants
- Types: Integer Mode, Real Mode, Mixed Mode

### 3.5 Integer and Float Conversions
1. Integer ÷ Integer = Integer
2. Real ÷ Real = Real
3. Integer ÷ Real = Real (integer promoted first)

### 3.6 Type Conversions
1. **Implicit**: Automatic type changes when needed
2. **Promotion**: Smaller types promoted to int
3. **Assignment**: Type converted to match variable type
4. **Casting**: Explicit conversion using `(type_name)`

### 3.7 Hierarchy of Operations
**Priority Order:**
1. `()`: Brackets
2. `*`, `/`, `%`: Multiplication, division, modulus
3. `+`, `-`: Addition, subtraction
4. `=`: Assignment

### 3.8 Associativity of Operations
- **Operator Precedence**: Evaluation order based on priority
- **Associativity**: Order for same precedence operators
- Most operators: Left-to-right
- Assignment, unary: Right-to-left

### 3.9 Shorthand Operators
- `+=`: Addition assignment
- `-=`: Subtraction assignment
- `*=`: Multiplication assignment
- `/=`: Division assignment
- `%=`: Remainder assignment

### 3.10 Unary Operators
- `-`: Negation
- `++`: Increment
- `--`: Decrement
- Types: Pre-increment/decrement, Post-increment/decrement

### 3.11 Control Instructions
1. **Sequence**: Execute in written order
2. **Selection**: Choose instructions based on conditions (`if-else`)
3. **Loop**: Repeat instructions (`for`, `while`)
4. **Case**: Execute from multiple options (`switch`)

## 4. Decision Control Structure

### 4.1 What is Decision Control?
1. Conditional execution based on conditions
2. Handles complex decisions through nesting
3. Increases program adaptability

### 4.2 Relational Operator
- `==`: Equality
- `!=`: Inequality
- `>`: Greater than
- `<`: Less than
- `>=`: Greater than or equal
- `<=`: Less than or equal

### 4.3 if Statement
- Syntax: `if (condition) { }`
- Executes block if condition true
- Curly braces optional for single statements (not recommended)
- Can store conditions in variables

### 4.4 Truthy vs Falsy
- **Falsy**: `0` and `NULL`
- **Truthy**: Any non-zero value
- Used in `if`, `while`, `for` conditions
- Automatic conversion based on numeric value

### 4.5 if-else
- `else` executes when `if` condition is false
- Provides alternative execution path

### 4.6 if-else-if Ladder
1. Sequential condition checking
2. Executes first true condition's block
3. Exits after finding true condition
4. Final `else` as default case

### 4.7 Nested if
- `if` inside another `if` or `else`
- Enables hierarchical condition checks
- Allows detailed decision paths
- Deep nesting can reduce readability

### 4.8 Logical Operators
- `&&`: AND (all conditions must be true)
- `||`: OR (at least one condition true)
- `!`: NOT (inverts condition)
- Lower priority than arithmetic/comparison

### 4.9 Ternary Operator
- Syntax: `condition ? expression1 : expression2`
- Boolean condition evaluation
- Both expressions must return compatible types
- Good for simple assignments

### 4.10 Switch
- Cleaner multi-way branching than multiple if-else
- Expression must be integer or character
- `case` labels represent branches
- `break` prevents fall-through
- `default` case for no matches

### 4.11 Goto Statement
- Unconditional jump to label
- Label defined with name and colon
- Must be in same function
- Useful for error handling, nested loop exiting
- Generally discouraged

## 5. Iteration & Loop Control Structure

### 5.1 Need of Loops
1. Code runs multiple times based on condition
2. Repeated execution automation
3. Automates repetitive tasks
4. Types: `while`, `for`, `do-while`
5. Iterations: Number of loop executions

### 5.2 While Loop
- Repeats while condition is true
- Used for non-standard conditions
- Must include update to avoid infinite loops

### 5.3 For Loop
- Standard loop for counting iterations
- Preferred when number of iterations known
- Syntax: `for (initialization; condition; update)`

### 5.4 Break Statement
- Stops loop early or breaks out
- Exits loops and switch cases
- Immediate effect
- Alters program flow

### 5.5 Continue Statement
- Skips current iteration
- Starts next iteration immediately
- In while loop, increment manually before continue
- Helps avoid nested conditions

### 5.6 Odd Loop
- Runs unknown number of times
- Condition-driven
- Uses `while` and `do-while`
- May use `break` for exit
- Design carefully to avoid infinite loops

### 5.7 Do-while Loop
- Executes block first, then checks condition
- Guaranteed at least one iteration
- Unlike while, first iteration unconditional
- Update condition to avoid infinite loops

### 5.8 Infinite Loop
- Endless execution
- Purposeful or accidental
- Requires `break` or similar to stop
- May cause high CPU usage

## 6. Function and Recursion

### 6.1 What is a Function?
1. Blocks of reusable code
2. DRY Principle: "Don't Repeat Yourself"
3. Organizes code and performs tasks
4. Naming rules: snake_case
5. Example: Modular code components

### 6.2 Function Prototype
- Specifies name, return type, parameters without body
- Enables type checking and forward declaration
- Parameter names optional in prototypes
- Placed at file start or in header files

### 6.3 Function Syntax / Definition
- Follows variable naming rules
- Uses `()` for parameters
- Fundamental for code organization and reusability
- Contains function header and body

### 6.4 Function Call
- Invoke using function name followed by `()`
- Executes function code
- Can pass arguments

### 6.5 Return Statement
1. Sends value back from function
2. Can return values, variables, calculations
3. Ends function immediately
4. Function calls make code jump around
5. Prefer returning values over global variables

### 6.6 Passing Values
1. Input values function takes
2. Parameters put values in, return gets values out
3. Multiple parameters possible
4. Same naming conventions as variables

### 6.7 Argument vs Parameter
- **Parameters**: Variables in function definition (placeholders)
- **Arguments**: Actual values passed at call time

### 6.8 Call by Value
1. Passes argument's copy, not original
2. Parameters use separate memory
3. Original data unchanged
4. Cannot modify original arguments directly
5. Good for small data types

### 6.9 Scoping Rule
1. **Local Scope**: Variables inside functions, not accessible outside
2. **Global Scope**: Variables outside functions, accessible anywhere in file
3. **Block Scope**: Variables in blocks accessible only within blocks
4. **Function Parameters**: Act as local variables
5. **Lifetime**: Local variables exist during function execution only

### 6.10 Recursion
1. **Self-Calling**: Function calls itself
2. **Base Case**: Essential to stop recursion
3. **Recursive Case**: Condition for continued calling
4. **Stack Usage**: Consumes stack space, risk of overflow
5. **Applications**: Tree/graph traversals, sorting algorithms
6. **Memory Intensive**: More overhead than iterative solutions
7. **Clarity**: Simplifies complex problems

## 7. Pointers

### 7.1 Introduction to Pointers
- Store memory addresses of other variables
- Rather than storing data itself
- Powerful feature for memory manipulation

### 7.2 & (Address) Operator
- Ampersand `&` gets variable's address
- Returns memory location where variable stored

### 7.3 * (Value at address) Operator
- Asterisk `*` gets value from particular address
- Called "value at address" or "dereference" operator

### 7.4 Pointer Declaration
- Declared with asterisk before variable name
- Example: `int *ptr;`
- Stores memory addresses

### 7.5 Pointer to a Pointer
- Pointer that stores address of another pointer
- Allows indirect access to variable value
- Multiple levels of indirection possible

### 7.6 Call By Reference
1. Passes address of variables
2. Functions can modify actual values
3. Implemented using pointers
4. Avoids copying large data structures
5. Can return multiple values via out-parameters
6. Risk of unintended side effects

## 8. Data Types and Storage Classes

### 8.1 Long
- Larger than int (64-bit on 64-bit systems, 32-bit on 32-bit systems)
- Holds larger integer values
- Suffix: `L` or `l` for long literals (e.g., `100L`)
- `long long` variant for even larger integers
- Guaranteed at least 32 bits by C standard

### 8.2 Signed and Unsigned
- **Signed int**: Positive and negative numbers including zero
- **Unsigned int**: Only non-negative numbers (doubles positive range)
- **Range**: Signed: -2³¹ to 2³¹-1, Unsigned: 0 to 2³²-1 (32-bit)
- **Overflow**: Unsigned wraps around
- **Usage**: Unsigned for countable quantities

### 8.3 What are Storage Classes
1. **Lifetime Management**: Determine variable scope and duration
2. **Scope Control**: Dictate variable accessibility
3. **Memory Location**: Influence storage location (stack, heap, data segment)
4. **Initialization**: Define default initial values

### 8.4 Automatic (auto)
- Default for local variables within functions
- Stored on stack
- Local to block where defined
- Undefined initial value unless explicitly initialized
- Created when block entered, destroyed when exited

### 8.5 Register
- Hints compiler to store in CPU register for faster access
- Limited to variables that fit in registers
- No memory address (can't use `&`)
- Local to function/block
- For heavily used variables like loop counters

### 8.6 Static
- Retains value between function calls
- Automatically initialized to zero if no initial value
- Can be local to function or have file scope
- File-scope: visible only within declaring file
- Single instance, not recreated each call

### 8.7 External (extern)
- Defined in another file or outside functions
- Shared across multiple files
- Declaration references memory location without allocation
- Typically not initialized with declaration
- Useful for global variables accessed by multiple functions

### 8.8 Usage of Storage Classes
1. **auto**: Default for local variables, limited block scope/lifetime
2. **register**: Heavily used variables, compiler may ignore hint
3. **static**: Retain value between calls, limit file visibility
4. **extern**: Access variables across files, shared data

## 9. Arrays

### 9.1 Need of Array
- List of values
- Index starts with 0
- Store multiple values in single variable
- Efficient data organization

### 9.2 Array Declaration
- Syntax: `type name[size];` (e.g., `int arr[10];`)
- Fixed size (known at compile time)
- Zero-based indexing
- Contiguous memory block
- All elements same type

### 9.3 Accessing Array Elements
- Use indexes: `arr[index]`
- Start at 0: `arr[0]` is first element
- Use loops for iteration
- No automatic bounds checking

### 9.4 Array Initialization
- Direct: `int nums[] = {1, 2, 3};`
- Auto zero-fill: `int arr[5] = {1};` (others become 0)
- Zero array: `int arr[5] = {0};`
- Designated: `int arr[5] = {[2] = 5};`

### 9.5 Array Traversal
- Orderly visit from start to end
- Use `for` or `while` loops
- Indexes: 0 to size-1
- Modify or read elements
- Pointer arithmetic option

### 9.6 Bounds Checking
- C doesn't auto-check array bounds
- Programmer must ensure valid indices
- Out-of-bounds access can cause crashes/security issues
- Always validate indices against array size

### 9.7 Array as Function Arguments
- Arrays become pointers when passed to functions
- Call by reference (changes affect original)
- Pass array size as extra argument
- Specify element type in parameters
- Efficient (only pointer passed, no full copy)

### 9.8 Pointer Arithmetic
- `*(arr + i)` equals `arr[i]`
- `ptr++` or `ptr--` moves pointer based on type size
- Adding/subtracting integers moves pointer by elements
- Pointer subtraction gives number of elements between

### 9.9 Pointers and Arrays
- Array name acts as constant pointer to first element
- Array decays to pointer when passed to functions
- Can access elements via pointer arithmetic

### 9.10 Two-Dimensional Array
- Array of arrays (matrices/grids)
- Declaration: `int arr[3][4];` (3 rows, 4 columns)
- Initialization: `int arr[2][2] = {{1, 2}, {3, 4}};`
- Access: `arr[row][column]`
- Row-major order storage

### 9.11 Multi-Dimensional Array
- Extension to more dimensions (3D+, cubes)
- Declaration: `int arr[2][3][4];` (3D array)
- Nested braces initialization
- Access: `arr[x][y][z]`
- Row-major order continues

## 10. Strings

### 10.1 What is a String
- Sequence of characters terminated by null character `\0`
- Null character marks end (not included in length)
- String literals in double quotes: `"Hello, World!"`
- Mutable when stored in character arrays

### 10.2 String Memory Allocation
- Fixed size at compile time (includes null terminator)
- Contiguous memory storage like arrays
- Pre-allocated memory blocks

### 10.3 String Initialization
```c
char c[] = "abcd";
char c[50] = "abcd";
char c[] = {'a','b','c','d','\0'};
char c[5] = {'a','b','c','d','\0'};
```

### 10.4 Format Specifiers
- Output: `%s` with `printf`
- Input: `%s` with `scanf` (stops at whitespace/newline/EOF)
- No `&` with `scanf` for strings (array name acts as pointer)
- Safety: Specify field width (e.g., `%49s` for 50-char array)

### 10.5 fgets and puts functions
**fgets():**
- Safe input from file/stdin into buffer
- Limits length to prevent overflow
- Can include newline if fits in buffer

**puts():**
- Simple output to stdout
- Appends newline automatically
- No formatting options

**gets() (Not Recommended):**
- Unsafe (no size limits)
- Prone to buffer overflow
- Removed from C11 standard

### 10.6 Pointers and Strings
- String represented as pointer to first character
- Example: `char *str = "Hello";`
- String literals immutable when assigned to pointers
- Character arrays allow modification

### 10.7 String.h Functions
**strlen():**
- Returns string length excluding null terminator

**strcpy():**
- Copies source string to destination including null terminator

**strcat():**
- Appends source to destination
- Overwrites destination's null terminator, adds new one

**strcmp():**
- Compares strings lexicographically
- Returns integer based on comparison

### 10.8 2-D Array of Characters
- Matrix where each row represents a string
- Store multiple strings of same maximum length
- Each string must end with null character `\0`
- Fixed width defined by column size
- Access: `charArray[row]` for string, `charArray[row][col]` for character

## 11. Structures

### 11.1 Why use Structure
1. Group related data items of different types
2. Model real-world entities naturally
3. Simplify passing multiple data as single argument
4. Enhance code readability and maintainability
5. Create new data types for specific needs

### 11.2 Structure Declaration
- Use `struct` keyword
- Optional tag name
- Member declarations in braces `{}`
- End with semicolon `;`

### 11.3 Accessing Structure Elements
- Dot operator: `structure.member`
- Nested access: `outer.inner.member`
- Direct member access

### 11.4 Structure Memory Allocation
- Contiguous memory spaces
- Compiler may add padding for alignment
- Use `sizeof` to get actual size (padding included)
- Members stored in declaration order

### 11.5 Structure Initialization
- Direct: `struct Student s1 = {1, "Alice", 85.5};`
- Designated (C99): `struct Student s2 = {.rollno=2, .name="Bob", .marks=90.2};`
- Zero: `struct Student s3 = {0};`
- Copy: `struct Student s4 = s1;`

### 11.6 Array of Structures
- Array where each element is a structure
- Store multiple records of same type
- Access: `array[index].member`
- Useful for database-like data

### 11.7 Structure Pointers
- Pointers that point to structure variables
- Same pointer arithmetic as structure arrays
- Access members via pointer

### 11.8 Arrow -> Operator
- Access structure members through pointer
- Syntax: `pointer->member`
- Equivalent to `(*pointer).member`
- More concise than dereferencing
- Common in linked lists

### 11.9 Structure as Function Arguments
- **Direct passing**: Copies whole structure (less efficient)
- **Pass by address**: More efficient, allows modifications
- **Performance**: Address passing faster for large structures
- **Simplicity**: Direct passing simpler but less flexible

### 11.10 Typedef keyword
- Creates aliases for existing types
- Simplifies structure syntax
- Enhances code readability
- Facilitates portability across systems

## 12. Dynamic Memory Allocation

### 12.1 What is Dynamic Memory Allocation
1. **Flexibility**: Allocate memory at runtime as needed
2. **Efficiency**: Use only necessary memory, release when done
3. **Persistence**: Memory persists beyond creation scope until freed
4. **Large Data**: Handle datasets exceeding stack size
5. **Data Structures**: Essential for linked lists, trees, graphs

### 12.2 Using malloc
- Include `stdlib.h` header
- Pass size in bytes to allocate
- Cast returned `void*` to appropriate type
- Check for `NULL` (allocation failure)
- Does not initialize memory (may contain garbage)

### 12.3 Using calloc
- Initializes all allocated memory to zero
- Takes two arguments: number of elements, element size
- Preferred for array allocation with zero-initialization
- Slightly more overhead than malloc
- Returns `void*` pointer (should be cast)

### 12.4 Using free
- Deallocates previously allocated memory
- Essential for preventing memory leaks
- Takes pointer to allocated memory block
- Safe to call with `NULL` pointer (no operation)
- Pointer should not be used after freeing

### 12.5 Using realloc
- Resizes previously allocated memory
- Preserves existing data when possible
- If passed `NULL`, behaves like `malloc`
- If size is 0, behaves like `free`
- Returns new pointer (may differ from original)
- Check return value before use

## 13. File Input/Output

### 13.1 Data Organization
**Storage Types:**
1. **RAM**: Volatile, temporary data storage
2. **ROM**: Non-volatile, firmware storage
3. **HDDs**: Mechanical, magnetic, long-term storage
4. **SSDs**: Fast, non-volatile, flash memory
5. **Cache**: Speedy volatile memory in CPUs
6. **Virtual Memory**: Hard drive used as RAM extension
7. **Flash Memory**: Portable non-volatile storage
8. **Optical Storage**: CDs, DVDs, Blu-ray discs

**C Library Benefits:**
1. **Simplicity**: Simple interface hiding OS complexity
2. **Portability**: Same calls across different OS
3. **Standardization**: Consistent behavior across environments
4. **Ease of Use**: No OS-specific system call knowledge needed
5. **Abstraction**: Manages OS interactions seamlessly

### 13.2 File Operations
1. **Creation**: Establish new file on disk
2. **Opening**: Acquire access to existing file
3. **Reading**: Retrieve data from file
4. **Writing**: Output data to file
5. **Seeking**: Move to specific file location
6. **Closing**: Release file and resources

### 13.3 Text Files & Binary Files
- **Text Files**: Human-readable, character representation
- **Binary Files**: Same as in-memory representation, byte sequence
- **Portability**: Text files more portable across platforms
- **Efficiency**: Binary files more efficient for I/O operations

### 13.4 File pointer
- Type: `FILE*`
- Standard: `stdin`, `stdout`, `stderr`
- Associated with file via `fopen`
- Used for reading/writing operations
- Tracks current file position
- Should be passed to `fclose`

### 13.5 Open a File
- `fopen()` function returns `FILE*` pointer
- Modes: `r` (read), `w` (write), `a` (append), etc.
- Returns `NULL` on failure
- Always check for successful opening
- Can use relative or absolute paths

### 13.6 Close a File
- `fclose()` closes open file
- Releases system resources
- Flushes any remaining buffer data
- Good practice to set pointer to `NULL` after closing
- Check return value for success (0) or error (EOF)

### 13.7 Reading data from File
- Functions: `fgetc`, `fgets`, `fread`, `fscanf`
- Modes: `"r"` (read), `"r+"` (read/update)
- Ensure proper buffer sizing
- Choose functions based on file type (text/binary)

### 13.8 End of File (EOF)
- Constant indicating file end or error
- Typically `-1` in C libraries
- Used by functions like `fgetc()` for end detection
- Can signal operation failures
- Common in file reading loops

### 13.9 Writing data to a File
- Functions: `fputc`, `fputs`, `fwrite`, `fprintf`
- Modes: `"w"` (write), `"a"` (append), `"w+"`, `"a+"` (update)
- `fflush()` forces buffer write to file
- Choose function/mode based on file type

### 13.10 Appending data to a File
- Open file in append mode (`"a"` or `"a+"`)
- New data added to end of file
- Existing content preserved
- File position set to end for writing

### 13.11 File Opening Modes
- `"r"`: Read (file must exist)
- `"w"`: Write (creates/truncates file)
- `"a"`: Append (creates/appends to file)
- `"r+"`: Read/update (file must exist)
- `"w+"`: Write/update (creates/truncates file)
- `"a+"`: Append/update (creates/appends to file)

## ##. Most Used Basic Topics

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

### **Character Handling Functions**

####  ctype.h Functions
```c
#include <stdio.h>
#include <ctype.h>

int main() {
    char ch = 'A';
    
    printf("isalpha('%c'): %d\n", ch, isalpha(ch));
    printf("isdigit('%c'): %d\n", ch, isdigit(ch));
    printf("isupper('%c'): %d\n", ch, isupper(ch));
    printf("islower('%c'): %d\n", ch, islower(ch));
    printf("isspace('%c'): %d\n", ch, isspace(ch));
    
    // Conversion functions
    printf("tolower('%c'): %c\n", ch, tolower(ch));
    printf("toupper('%c'): %c\n", 'b', toupper('b'));
    
    return 0;
}
```

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

###  **String Manipulation Basics**

####  Basic String Functions
```c
#include <stdio.h>
#include <string.h>

int main() {
    char str1[20] = "Hello";
    char str2[20] = "World";
    char str3[40];
    
    // String length
    printf("Length of '%s': %zu\n", str1, strlen(str1));
    
    // String copy
    strcpy(str3, str1);
    printf("After strcpy: %s\n", str3);
    
    // String concatenation
    strcat(str3, " ");
    strcat(str3, str2);
    printf("After strcat: %s\n", str3);
    
    // String comparison
    int cmp = strcmp(str1, str2);
    if (cmp < 0) {
        printf("'%s' comes before '%s'\n", str1, str2);
    } else if (cmp > 0) {
        printf("'%s' comes after '%s'\n", str1, str2);
    } else {
        printf("Strings are equal\n");
    }
    
    // String search
    char *found = strchr(str3, 'W');
    if (found) {
        printf("Found 'W' at position: %ld\n", found - str3);
    }
    
    return 0;
}
```

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

###  **Basic Error Handling**

####  Return Value Checking
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    FILE *file;
    int *ptr;
    
    // File opening error handling
    file = fopen("nonexistent.txt", "r");
    if (file == NULL) {
        perror("Error opening file");
        // Handle error appropriately
    }
    
    // Memory allocation error handling
    ptr = (int*)malloc(1000000000 * sizeof(int));  // Very large allocation
    if (ptr == NULL) {
        fprintf(stderr, "Memory allocation failed!\n");
        exit(EXIT_FAILURE);
    }
    
    // Always free allocated memory
    free(ptr);
    
    return 0;
}
```

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

## 14. Preprocessor Directives

### 14.1 What are Preprocessor Directives
- Processed before compilation
- Begin with `#` symbol
- Text substitution and file inclusion
- No semicolon required

### 14.2 ` #include ` Directive
```c
#include <stdio.h>    // System header files
#include "myheader.h" // User header files
```
- Copies entire content of included file
- Angle brackets for system headers
- Quotes for user-defined headers

### 14.3 `#define` Directive
**Macro Definitions:**
```c
#define PI 3.14159
#define MAX(a, b) ((a) > (b) ? (a) : (b))
#define SQUARE(x) ((x) * (x))
```

**Advantages:**
- No function call overhead
- Type-independent
- Compile-time evaluation

**Pitfalls:**
```c
#define SQUARE(x) x * x
SQUARE(5 + 3) // Expands to: 5 + 3 * 5 + 3 = 23 (not 64)
```

### 14.4 Conditional Compilation
```c
#ifdef DEBUG
    printf("Debug: x = %d\n", x);
#endif

#ifndef VERSION
    #define VERSION "1.0"
#endif

#if LEVEL == 1
    // Code for level 1
#elif LEVEL == 2
    // Code for level 2
#else
    // Default code
#endif
```

### 14.5 `#undef` Directive
```c
#define TEMP 100
#undef TEMP
// TEMP is no longer defined
```

### 14.6 Predefined Macros
```c
printf("File: %s\n", __FILE__);
printf("Line: %d\n", __LINE__);
printf("Date: %s\n", __DATE__);
printf("Time: %s\n", __TIME__);
printf("Function: %s\n", __func__);
```

## 15. Command Line Arguments

### 15.1 main() Function with Arguments
```c
int main(int argc, char *argv[]) {
    // argc: argument count
    // argv: argument vector
    return 0;
}
```

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

## 16. Bitwise Operations

### 16.1 Bitwise Operators
- `&` : AND
- `|` : OR
- `^` : XOR
- `~` : NOT (One's complement)
- `<<` : Left shift
- `>>` : Right shift

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

### 16.3 Common Bit Manipulation Techniques
```c
// Set bit n
x |= (1 << n);

// Clear bit n
x &= ~(1 << n);

// Toggle bit n
x ^= (1 << n);

// Check if bit n is set
if (x & (1 << n)) {
    // Bit is set
}

// Count set bits (Brian Kernighan's algorithm)
int countSetBits(unsigned int n) {
    int count = 0;
    while (n) {
        n &= (n - 1);
        count++;
    }
    return count;
}
```

## 17. Unions

### 17.1 What are Unions
- Similar to structures but share memory
- All members share same memory location
- Size equals largest member size

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

## 18. Enumerations

### 18.1 Enum Declaration
```c
enum Weekdays {
    MONDAY,    // 0
    TUESDAY,   // 1
    WEDNESDAY, // 2
    THURSDAY,  // 3
    FRIDAY,    // 4
    SATURDAY,  // 5
    SUNDAY     // 6
};

enum Colors {
    RED = 1,
    GREEN = 2,
    BLUE = 4,
    YELLOW = RED | GREEN,  // 3
    WHITE = RED | GREEN | BLUE  // 7
};
```

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

## 19. Error Handling

### 19.1 errno and perror
```c
#include <stdio.h>
#include <errno.h>
#include <string.h>

int main() {
    FILE *file = fopen("nonexistent.txt", "r");
    
    if (file == NULL) {
        printf("Error number: %d\n", errno);
        perror("Error message");
        printf("Error description: %s\n", strerror(errno));
    }
    
    return 0;
}
```

### 19.2 Custom Error Handling
```c
#include <stdio.h>
#include <stdlib.h>

typedef enum {
    SUCCESS,
    ERROR_NULL_POINTER,
    ERROR_INVALID_INPUT,
    ERROR_OUT_OF_MEMORY
} ErrorCode;

const char* getErrorMessage(ErrorCode code) {
    switch (code) {
        case SUCCESS: return "Success";
        case ERROR_NULL_POINTER: return "Null pointer error";
        case ERROR_INVALID_INPUT: return "Invalid input";
        case ERROR_OUT_OF_MEMORY: return "Out of memory";
        default: return "Unknown error";
    }
}

ErrorCode safeDivide(int a, int b, double *result) {
    if (result == NULL) {
        return ERROR_NULL_POINTER;
    }
    
    if (b == 0) {
        return ERROR_INVALID_INPUT;
    }
    
    *result = (double)a / b;
    return SUCCESS;
}

int main() {
    double result;
    ErrorCode error = safeDivide(10, 0, &result);
    
    if (error != SUCCESS) {
        printf("Error: %s\n", getErrorMessage(error));
        return 1;
    }
    
    printf("Result: %.2f\n", result);
    return 0;
}
```

## 20. Variable Length Arrays (VLAs)

### 20.1 VLA Declaration
```c
#include <stdio.h>

void printArray(int rows, int cols, int arr[rows][cols]) {
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            printf("%d ", arr[i][j]);
        }
        printf("\n");
    }
}

int main() {
    int rows, cols;
    
    printf("Enter number of rows: ");
    scanf("%d", &rows);
    printf("Enter number of columns: ");
    scanf("%d", &cols);
    
    int arr[rows][cols];  // VLA
    
    // Initialize array
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            arr[i][j] = i * cols + j;
        }
    }
    
    printArray(rows, cols, arr);
    return 0;
}
```

## 21. Inline Functions

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

## 22. Complex Numbers (C99)

### 22.1 Complex Number Operations
```c
#include <stdio.h>
#include <complex.h>

int main() {
    double complex z1 = 3.0 + 4.0 * I;
    double complex z2 = 1.0 - 2.0 * I;
    
    double complex sum = z1 + z2;
    double complex product = z1 * z2;
    double complex conjugate = conj(z1);
    
    printf("z1 = %.2f + %.2fi\n", creal(z1), cimag(z1));
    printf("z2 = %.2f + %.2fi\n", creal(z2), cimag(z2));
    printf("Sum = %.2f + %.2fi\n", creal(sum), cimag(sum));
    printf("Product = %.2f + %.2fi\n", creal(product), cimag(product));
    printf("Conjugate of z1 = %.2f + %.2fi\n", creal(conjugate), cimag(conjugate));
    printf("Magnitude of z1 = %.2f\n", cabs(z1));
    
    return 0;
}
```

## 23. Type Qualifiers

### 23.1 const Qualifier
```c
#include <stdio.h>

// const with pointers
void demonstrateConst() {
    int value = 10;
    int another = 20;
    
    // Pointer to constant integer
    const int *ptr1 = &value;
    // *ptr1 = 30;  // Error: cannot modify through ptr1
    ptr1 = &another;  // OK: can change what ptr1 points to
    
    // Constant pointer to integer
    int *const ptr2 = &value;
    *ptr2 = 30;      // OK: can modify value
    // ptr2 = &another;  // Error: cannot change what ptr2 points to
    
    // Constant pointer to constant integer
    const int *const ptr3 = &value;
    // *ptr3 = 40;       // Error: cannot modify
    // ptr3 = &another;  // Error: cannot change pointer
}
```

### 23.2 volatile Qualifier
```c
#include <stdio.h>

volatile int hardware_register;

void readHardware() {
    // volatile tells compiler this value might change unexpectedly
    int value = hardware_register;
    // Compiler won't optimize away this read
}

int main() {
    // Simulate hardware changing the register
    for (int i = 0; i < 10; i++) {
        hardware_register = i;
        readHardware();
    }
    return 0;
}
```

### 23.3 restrict Qualifier (C99)
```c
#include <stdio.h>

// restrict indicates pointers don't alias
void copyArray(int n, int *restrict dest, const int *restrict src) {
    for (int i = 0; i < n; i++) {
        dest[i] = src[i];  // Compiler can optimize better
    }
}

int main() {
    int src[] = {1, 2, 3, 4, 5};
    int dest[5];
    
    copyArray(5, dest, src);
    
    for (int i = 0; i < 5; i++) {
        printf("%d ", dest[i]);
    }
    printf("\n");
    
    return 0;
}
```

## 24. Multi-file Programming

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

### 24.2 Implementation File (math_utils.c)
```c
#include "math_utils.h"

int add(int a, int b) {
    return a + b;
}

int subtract(int a, int b) {
    return a - b;
}

int multiply(int a, int b) {
    return a * b;
}

double divide(int a, int b) {
    if (b == 0) {
        return 0.0;  // Simple error handling
    }
    return (double)a / b;
}
```

### 24.3 Main File (main.c)
```c
#include <stdio.h>
#include "math_utils.h"

int main() {
    int x = 10, y = 5;
    
    printf("%d + %d = %d\n", x, y, add(x, y));
    printf("%d - %d = %d\n", x, y, subtract(x, y));
    printf("%d * %d = %d\n", x, y, multiply(x, y));
    printf("%d / %d = %.2f\n", x, y, divide(x, y));
    printf("Square of %d: %d\n", x, square(x));
    printf("PI: %.5f\n", PI);
    
    return 0;
}
```

### 24.4 Compilation
```bash
gcc -c math_utils.c -o math_utils.o
gcc -c main.c -o main.o
gcc math_utils.o main.o -o program
./program
```

## 25. Advanced Memory Management

### 25.1 Memory Pool Allocator
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define POOL_SIZE 1024

typedef struct {
    char pool[POOL_SIZE];
    size_t used;
} MemoryPool;

void* pool_alloc(MemoryPool *pool, size_t size) {
    if (pool->used + size > POOL_SIZE) {
        return NULL;  // Out of memory
    }
    
    void *ptr = pool->pool + pool->used;
    pool->used += size;
    return ptr;
}

void pool_reset(MemoryPool *pool) {
    pool->used = 0;
}

int main() {
    MemoryPool pool = {0};
    
    int *numbers = pool_alloc(&pool, 10 * sizeof(int));
    char *text = pool_alloc(&pool, 100 * sizeof(char));
    
    if (numbers && text) {
        for (int i = 0; i < 10; i++) {
            numbers[i] = i * i;
        }
        
        strcpy(text, "Hello from memory pool!");
        
        printf("Numbers: ");
        for (int i = 0; i < 10; i++) {
            printf("%d ", numbers[i]);
        }
        printf("\nText: %s\n", text);
    }
    
    pool_reset(&pool);  // Reset for reuse
    
    return 0;
}
```

## 26. Signal Handling

### 26.1 Basic Signal Handling
```c
#include <stdio.h>
#include <stdlib.h>
#include <signal.h>
#include <unistd.h>

void signal_handler(int sig) {
    switch (sig) {
        case SIGINT:
            printf("\nReceived SIGINT (Ctrl+C). Cleaning up...\n");
            exit(0);
        case SIGTERM:
            printf("Received SIGTERM. Exiting gracefully...\n");
            exit(0);
        case SIGUSR1:
            printf("Received SIGUSR1. Custom action.\n");
            break;
    }
}

int main() {
    // Register signal handlers
    signal(SIGINT, signal_handler);
    signal(SIGTERM, signal_handler);
    signal(SIGUSR1, signal_handler);
    
    printf("Program started. PID: %d\n", getpid());
    printf("Send SIGUSR1: kill -USR1 %d\n", getpid());
    printf("Press Ctrl+C to exit.\n");
    
    while (1) {
        printf("Working...\n");
        sleep(2);
    }
    
    return 0;
}
```

## 27. Advanced File Operations

### 27.1 Random File Access
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    int id;
    char name[50];
    double salary;
} Employee;

void writeEmployees() {
    FILE *file = fopen("employees.dat", "wb");
    if (!file) {
        perror("Failed to open file");
        return;
    }
    
    Employee employees[] = {
        {1, "John Doe", 50000.0},
        {2, "Jane Smith", 60000.0},
        {3, "Bob Johnson", 55000.0}
    };
    
    fwrite(employees, sizeof(Employee), 3, file);
    fclose(file);
}

void readEmployee(int recordNum) {
    FILE *file = fopen("employees.dat", "rb");
    if (!file) {
        perror("Failed to open file");
        return;
    }
    
    Employee emp;
    
    // Seek to specific record
    fseek(file, (recordNum - 1) * sizeof(Employee), SEEK_SET);
    
    if (fread(&emp, sizeof(Employee), 1, file) == 1) {
        printf("Record %d: ID=%d, Name=%s, Salary=%.2f\n", 
               recordNum, emp.id, emp.name, emp.salary);
    } else {
        printf("Record %d not found\n", recordNum);
    }
    
    fclose(file);
}

int main() {
    writeEmployees();
    
    printf("Reading individual records:\n");
    readEmployee(1);
    readEmployee(2);
    readEmployee(3);
    
    return 0;
}
```

## 28. Function Pointers

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

## 29. Variadic Functions

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

## 30. Threading (with POSIX threads)

### 30.1 Basic Multithreading
```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <unistd.h>

#define NUM_THREADS 5

// Thread function
void* printHello(void* threadid) {
    long tid = (long)threadid;
    printf("Hello from thread %ld\n", tid);
    sleep(1);
    printf("Thread %ld finished\n", tid);
    pthread_exit(NULL);
}

int main() {
    pthread_t threads[NUM_THREADS];
    int rc;
    long t;
    
    for (t = 0; t < NUM_THREADS; t++) {
        printf("Creating thread %ld\n", t);
        rc = pthread_create(&threads[t], NULL, printHello, (void*)t);
        
        if (rc) {
            printf("Error creating thread %ld\n", t);
            exit(-1);
        }
    }
    
    // Wait for all threads to complete
    for (t = 0; t < NUM_THREADS; t++) {
        pthread_join(threads[t], NULL);
    }
    
    printf("All threads completed\n");
    pthread_exit(NULL);
}
```

## 31. Memory Alignment and Padding

### 31.1 Structure Padding
```c
#include <stdio.h>

struct Unaligned {
    char a;     // 1 byte
    int b;      // 4 bytes
    char c;     // 1 byte
}; // Size: 12 bytes (not 6) due to padding

struct Aligned {
    int b;      // 4 bytes
    char a;     // 1 byte
    char c;     // 1 byte
}; // Size: 8 bytes (better packing)

#pragma pack(push, 1)
struct Packed {
    char a;
    int b;
    char c;
}; // Size: 6 bytes (no padding)
#pragma pack(pop)

int main() {
    printf("Unaligned size: %lu\n", sizeof(struct Unaligned));
    printf("Aligned size: %lu\n", sizeof(struct Aligned));
    printf("Packed size: %lu\n", sizeof(struct Packed));
    
    return 0;
}
```

### 31.2 Memory Alignment Functions
```c
#include <stdio.h>
#include <stdlib.h>
#include <stdalign.h>

int main() {
    // C11 alignment features
    printf("max_align_t alignment: %zu\n", alignof(max_align_t));
    printf("double alignment: %zu\n", alignof(double));
    
    // Aligned memory allocation
    int *aligned_ptr = aligned_alloc(16, 1024); // 16-byte aligned
    if (aligned_ptr) {
        printf("Aligned pointer: %p\n", (void*)aligned_ptr);
        free(aligned_ptr);
    }
    
    return 0;
}
```

## 32. Atomic Operations (C11)

### 32.1 Atomic Variables
```c
#include <stdio.h>
#include <stdatomic.h>
#include <threads.h>

atomic_int counter = ATOMIC_VAR_INIT(0);

int increment_thread(void *arg) {
    for (int i = 0; i < 100000; i++) {
        atomic_fetch_add(&counter, 1);
    }
    return 0;
}

int main() {
    thrd_t t1, t2;
    
    thrd_create(&t1, increment_thread, NULL);
    thrd_create(&t2, increment_thread, NULL);
    
    thrd_join(t1, NULL);
    thrd_join(t2, NULL);
    
    printf("Final counter value: %d\n", atomic_load(&counter));
    printf("Expected: 200000\n");
    
    return 0;
}
```

### 32.2 Memory Ordering
```c
#include <stdatomic.h>
#include <stdio.h>

atomic_int data = ATOMIC_VAR_INIT(0);
atomic_int flag = ATOMIC_VAR_INIT(0);

void producer() {
    atomic_store_explicit(&data, 42, memory_order_relaxed);
    atomic_store_explicit(&flag, 1, memory_order_release);
}

void consumer() {
    while (atomic_load_explicit(&flag, memory_order_acquire) == 0) {
        // spin wait
    }
    int value = atomic_load_explicit(&data, memory_order_relaxed);
    printf("Consumed: %d\n", value);
}

int main() {
    producer();
    consumer();
    return 0;
}
```

## 33. Generic Programming (C11 _Generic)

### 33.1 Type-Generic Macros
```c
#include <stdio.h>

#define print_value(x) _Generic((x), \
    int: print_int, \
    double: print_double, \
    char*: print_string, \
    default: print_unknown \
)(x)

void print_int(int x) {
    printf("Integer: %d\n", x);
}

void print_double(double x) {
    printf("Double: %.2f\n", x);
}

void print_string(char* x) {
    printf("String: %s\n", x);
}

void print_unknown() {
    printf("Unknown type\n");
}

int main() {
    print_value(42);
    print_value(3.14159);
    print_value("Hello World");
    
    return 0;
}
```

### 33.2 Generic Math Functions
```c
#include <stdio.h>
#include <math.h>

#define SQUARE(x) _Generic((x), \
    int: square_int, \
    double: square_double, \
    float: square_float \
)(x)

int square_int(int x) { return x * x; }
double square_double(double x) { return x * x; }
float square_float(float x) { return x * x; }

int main() {
    printf("Square of 5: %d\n", SQUARE(5));
    printf("Square of 2.5: %.2f\n", SQUARE(2.5));
    printf("Square of 1.5f: %.2f\n", SQUARE(1.5f));
    
    return 0;
}
```

## 34. Static Analysis and Code Quality

### 34.1 Compiler Sanitizers
```c
// Compile with: gcc -fsanitize=address -fsanitize=undefined program.c

#include <stdio.h>
#include <stdlib.h>

void memory_errors() {
    // Buffer overflow
    int buffer[10];
    buffer[15] = 42;  // ASan will catch this
    
    // Use after free
    int *ptr = malloc(sizeof(int));
    free(ptr);
    *ptr = 10;  // ASan will catch this
    
    // Integer overflow
    int a = INT_MAX;
    a++;  // UBSan will catch this
}

int main() {
    memory_errors();
    return 0;
}
```

### 34.2 Static Assertions
```c
#include <stdio.h>
#include <assert.h>

// Compile-time assertions
static_assert(sizeof(int) == 4, "int must be 4 bytes");
static_assert(sizeof(long) >= 4, "long must be at least 4 bytes");

// Custom static assertion macro
#define STATIC_ASSERT(condition, message) \
    typedef char static_assert_##message[(condition) ? 1 : -1]

STATIC_ASSERT(sizeof(void*) == 8, "64_bit_required");

int main() {
    printf("All static assertions passed!\n");
    return 0;
}
```

## 35. Advanced Optimization Techniques

### 35.1 Loop Optimization
```c
#include <stdio.h>
#include <time.h>

#define SIZE 1000000

void unoptimized_loop(int *arr) {
    for (int i = 0; i < SIZE; i++) {
        arr[i] = i * 2 + 1;
    }
}

void optimized_loop(int *arr) {
    int *end = arr + SIZE;
    int value = 1;
    
    // Loop unrolling and pointer arithmetic
    while (arr < end - 3) {
        *arr++ = value; value += 2;
        *arr++ = value; value += 2;
        *arr++ = value; value += 2;
        *arr++ = value; value += 2;
    }
    
    // Handle remaining elements
    while (arr < end) {
        *arr++ = value; value += 2;
    }
}

int main() {
    int arr1[SIZE], arr2[SIZE];
    clock_t start, end;
    
    start = clock();
    unoptimized_loop(arr1);
    end = clock();
    printf("Unoptimized: %.6f seconds\n", (double)(end - start) / CLOCKS_PER_SEC);
    
    start = clock();
    optimized_loop(arr2);
    end = clock();
    printf("Optimized: %.6f seconds\n", (double)(end - start) / CLOCKS_PER_SEC);
    
    return 0;
}
```

### 35.2 Branch Prediction Optimization
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define SIZE 1000000

// Data that's mostly sorted (good for branch prediction)
void process_sorted_data() {
    int data[SIZE];
    int sum = 0;
    
    // Create mostly sorted data with some randomness
    for (int i = 0; i < SIZE; i++) {
        data[i] = i + (rand() % 10 - 5);  // Mostly increasing
    }
    
    clock_t start = clock();
    for (int i = 0; i < SIZE - 1; i++) {
        if (data[i] < data[i + 1]) {  // Usually true - predictable
            sum += data[i];
        }
    }
    clock_t end = clock();
    printf("Sorted data time: %.6f seconds\n", (double)(end - start) / CLOCKS_PER_SEC);
}

// Data that's random (bad for branch prediction)
void process_random_data() {
    int data[SIZE];
    int sum = 0;
    
    // Create random data
    for (int i = 0; i < SIZE; i++) {
        data[i] = rand() % 1000;
    }
    
    clock_t start = clock();
    for (int i = 0; i < SIZE - 1; i++) {
        if (data[i] < data[i + 1]) {  // 50/50 chance - unpredictable
            sum += data[i];
        }
    }
    clock_t end = clock();
    printf("Random data time: %.6f seconds\n", (double)(end - start) / CLOCKS_PER_SEC);
}

int main() {
    srand(time(NULL));
    process_sorted_data();
    process_random_data();
    return 0;
}
```

## 36. Embedded Systems Programming

### 36.1 Register Manipulation
```c
#include <stdint.h>

// Memory-mapped registers (typical in embedded systems)
#define GPIO_BASE 0x40020000UL
#define GPIO_MODER (*(volatile uint32_t*)(GPIO_BASE + 0x00))
#define GPIO_OTYPER (*(volatile uint32_t*)(GPIO_BASE + 0x04))
#define GPIO_OSPEEDR (*(volatile uint32_t*)(GPIO_BASE + 0x08))

// Bit manipulation macros
#define SET_BIT(reg, bit) ((reg) |= (1UL << (bit)))
#define CLEAR_BIT(reg, bit) ((reg) &= ~(1UL << (bit)))
#define TOGGLE_BIT(reg, bit) ((reg) ^= (1UL << (bit)))
#define READ_BIT(reg, bit) (((reg) >> (bit)) & 1UL)

void configure_led_pin() {
    // Set pin 5 as output (bits 10-11 in MODER register)
    CLEAR_BIT(GPIO_MODER, 11);
    SET_BIT(GPIO_MODER, 10);
    
    // Set output type to push-pull (bit 5 in OTYPER)
    CLEAR_BIT(GPIO_OTYPER, 5);
    
    // Set medium speed (bits 10-11 in OSPEEDR)
    SET_BIT(GPIO_OSPEEDR, 10);
    CLEAR_BIT(GPIO_OSPEEDR, 11);
}
```

### 36.2 Interrupt Service Routines
```c
#include <stdint.h>

// Interrupt vector table (simplified)
typedef void (*isr_function_t)(void);

// ISR function attributes (compiler-specific)
#define ISR __attribute__((interrupt))

// Example ISRs
ISR void systick_handler(void) {
    // System tick timer interrupt
    static uint32_t ticks = 0;
    ticks++;
    
    // Toggle LED every 1000 ticks
    if (ticks % 1000 == 0) {
        TOGGLE_BIT(GPIO_ODR, 5);  // Toggle LED pin
    }
}

ISR void uart_receive_handler(void) {
    // UART receive interrupt
    uint8_t data = UART_DR;  // Read received data
    
    // Echo back
    UART_DR = data;
}

// Interrupt vector table
isr_function_t vector_table[] __attribute__((section(".isr_vector"))) = {
    (isr_function_t)0x20001000,  // Initial stack pointer
    NULL,                        // Reset handler
    systick_handler,             // System tick timer
    uart_receive_handler,        // UART receive
    // ... more ISRs
};
```

## 37. Cryptography and Security

### 37.1 Simple Encryption Algorithms
```c
#include <stdio.h>
#include <string.h>
#include <stdint.h>

// XOR cipher (simple but insecure)
void xor_cipher(const uint8_t *input, uint8_t *output, size_t length, uint8_t key) {
    for (size_t i = 0; i < length; i++) {
        output[i] = input[i] ^ key;
    }
}

// Caesar cipher
void caesar_cipher(char *text, int shift) {
    for (int i = 0; text[i] != '\0'; i++) {
        if (text[i] >= 'A' && text[i] <= 'Z') {
            text[i] = 'A' + (text[i] - 'A' + shift) % 26;
        } else if (text[i] >= 'a' && text[i] <= 'z') {
            text[i] = 'a' + (text[i] - 'a' + shift) % 26;
        }
    }
}

// Simple hash function (FNV-1a)
uint32_t fnv1a_hash(const void *data, size_t length) {
    const uint8_t *bytes = (const uint8_t*)data;
    uint32_t hash = 2166136261u;  // FNV offset basis
    
    for (size_t i = 0; i < length; i++) {
        hash ^= bytes[i];
        hash *= 16777619u;  // FNV prime
    }
    
    return hash;
}

int main() {
    char message[] = "Hello, World!";
    uint8_t encrypted[sizeof(message)];
    
    printf("Original: %s\n", message);
    
    // XOR encryption
    xor_cipher((uint8_t*)message, encrypted, strlen(message), 0xAA);
    printf("XOR Encrypted: ");
    for (size_t i = 0; i < strlen(message); i++) {
        printf("%02X ", encrypted[i]);
    }
    printf("\n");
    
    // Caesar cipher
    caesar_cipher(message, 3);
    printf("Caesar Encrypted: %s\n", message);
    
    // Hash
    uint32_t hash = fnv1a_hash(message, strlen(message));
    printf("Hash: 0x%08X\n", hash);
    
    return 0;
}
```

## 38. Network Programming

### 38.1 Basic Socket Programming
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>

#define PORT 8080
#define BUFFER_SIZE 1024

void start_server() {
    int server_fd, new_socket;
    struct sockaddr_in address;
    int opt = 1;
    int addrlen = sizeof(address);
    char buffer[BUFFER_SIZE] = {0};
    char *hello = "Hello from server";
    
    // Create socket file descriptor
    if ((server_fd = socket(AF_INET, SOCK_STREAM, 0)) == 0) {
        perror("socket failed");
        exit(EXIT_FAILURE);
    }
    
    // Forcefully attach socket to the port 8080
    if (setsockopt(server_fd, SOL_SOCKET, SO_REUSEADDR | SO_REUSEPORT, &opt, sizeof(opt))) {
        perror("setsockopt");
        exit(EXIT_FAILURE);
    }
    
    address.sin_family = AF_INET;
    address.sin_addr.s_addr = INADDR_ANY;
    address.sin_port = htons(PORT);
    
    // Bind the socket to the network address and port
    if (bind(server_fd, (struct sockaddr *)&address, sizeof(address)) < 0) {
        perror("bind failed");
        exit(EXIT_FAILURE);
    }
    
    if (listen(server_fd, 3) < 0) {
        perror("listen");
        exit(EXIT_FAILURE);
    }
    
    printf("Server listening on port %d\n", PORT);
    
    if ((new_socket = accept(server_fd, (struct sockaddr *)&address, (socklen_t*)&addrlen)) < 0) {
        perror("accept");
        exit(EXIT_FAILURE);
    }
    
    // Read from client
    read(new_socket, buffer, BUFFER_SIZE);
    printf("Client: %s\n", buffer);
    
    // Send response
    send(new_socket, hello, strlen(hello), 0);
    printf("Hello message sent\n");
    
    close(new_socket);
    close(server_fd);
}
```

## 39. Performance Profiling and Benchmarking

### 39.1 High-Resolution Timing
```c
#include <stdio.h>
#include <time.h>

#ifdef _WIN32
    #include <windows.h>
#else
    #include <sys/time.h>
#endif

// Cross-platform high-resolution timer
typedef struct {
#ifdef _WIN32
    LARGE_INTEGER start;
    LARGE_INTEGER frequency;
#else
    struct timespec start;
#endif
} timer_t;

void timer_start(timer_t *timer) {
#ifdef _WIN32
    QueryPerformanceFrequency(&timer->frequency);
    QueryPerformanceCounter(&timer->start);
#else
    clock_gettime(CLOCK_MONOTONIC, &timer->start);
#endif
}

double timer_elapsed(timer_t *timer) {
#ifdef _WIN32
    LARGE_INTEGER end;
    QueryPerformanceCounter(&end);
    return (double)(end.QuadPart - timer->start.QuadPart) / timer->frequency.QuadPart;
#else
    struct timespec end;
    clock_gettime(CLOCK_MONOTONIC, &end);
    return (end.tv_sec - timer->start.tv_sec) + 
           (end.tv_nsec - timer->start.tv_nsec) / 1e9;
#endif
}

void benchmark_function() {
    timer_t timer;
    timer_start(&timer);
    
    // Code to benchmark
    volatile int sum = 0;
    for (int i = 0; i < 1000000; i++) {
        sum += i * i;
    }
    
    double elapsed = timer_elapsed(&timer);
    printf("Function took: %.6f seconds\n", elapsed);
    printf("Sum: %d\n", sum);
}

int main() {
    benchmark_function();
    return 0;
}
```

## 40. Advanced Data Structures

### 40.1 Red-Black Tree
```c
#include <stdio.h>
#include <stdlib.h>

typedef enum { RED, BLACK } Color;

typedef struct Node {
    int data;
    Color color;
    struct Node *left, *right, *parent;
} Node;

Node* create_node(int data) {
    Node* new_node = (Node*)malloc(sizeof(Node));
    new_node->data = data;
    new_node->color = RED;
    new_node->left = new_node->right = new_node->parent = NULL;
    return new_node;
}

void left_rotate(Node **root, Node *x) {
    Node *y = x->right;
    x->right = y->left;
    
    if (y->left != NULL)
        y->left->parent = x;
    
    y->parent = x->parent;
    
    if (x->parent == NULL)
        *root = y;
    else if (x == x->parent->left)
        x->parent->left = y;
    else
        x->parent->right = y;
    
    y->left = x;
    x->parent = y;
}

void right_rotate(Node **root, Node *y) {
    Node *x = y->left;
    y->left = x->right;
    
    if (x->right != NULL)
        x->right->parent = y;
    
    x->parent = y->parent;
    
    if (y->parent == NULL)
        *root = x;
    else if (y == y->parent->left)
        y->parent->left = x;
    else
        y->parent->right = x;
    
    x->right = y;
    y->parent = x;
}

void insert_fixup(Node **root, Node *z) {
    while (z != *root && z->parent->color == RED) {
        if (z->parent == z->parent->parent->left) {
            Node *y = z->parent->parent->right;
            
            if (y != NULL && y->color == RED) {
                z->parent->color = BLACK;
                y->color = BLACK;
                z->parent->parent->color = RED;
                z = z->parent->parent;
            } else {
                if (z == z->parent->right) {
                    z = z->parent;
                    left_rotate(root, z);
                }
                z->parent->color = BLACK;
                z->parent->parent->color = RED;
                right_rotate(root, z->parent->parent);
            }
        } else {
            // Symmetric case
            Node *y = z->parent->parent->left;
            
            if (y != NULL && y->color == RED) {
                z->parent->color = BLACK;
                y->color = BLACK;
                z->parent->parent->color = RED;
                z = z->parent->parent;
            } else {
                if (z == z->parent->left) {
                    z = z->parent;
                    right_rotate(root, z);
                }
                z->parent->color = BLACK;
                z->parent->parent->color = RED;
                left_rotate(root, z->parent->parent);
            }
        }
    }
    (*root)->color = BLACK;
}

void insert(Node **root, int data) {
    Node *z = create_node(data);
    Node *y = NULL;
    Node *x = *root;
    
    while (x != NULL) {
        y = x;
        if (z->data < x->data)
            x = x->left;
        else
            x = x->right;
    }
    
    z->parent = y;
    
    if (y == NULL)
        *root = z;
    else if (z->data < y->data)
        y->left = z;
    else
        y->right = z;
    
    insert_fixup(root, z);
}

void inorder_traversal(Node *root) {
    if (root != NULL) {
        inorder_traversal(root->left);
        printf("%d(%s) ", root->data, root->color == RED ? "RED" : "BLACK");
        inorder_traversal(root->right);
    }
}

int main() {
    Node *root = NULL;
    
    insert(&root, 10);
    insert(&root, 20);
    insert(&root, 30);
    insert(&root, 15);
    insert(&root, 25);
    
    printf("Red-Black Tree Inorder: ");
    inorder_traversal(root);
    printf("\n");
    
    return 0;
}
```

## 41. Metaprogramming and Code Generation

### 41.1 X-Macros
```c
#include <stdio.h>

// X-Macro for error codes
#define ERROR_TABLE \
    X(SUCCESS, "No error") \
    X(ERROR_INVALID_INPUT, "Invalid input provided") \
    X(ERROR_OUT_OF_MEMORY, "Memory allocation failed") \
    X(ERROR_FILE_NOT_FOUND, "File not found") \
    X(ERROR_NETWORK, "Network connection failed")

// Generate enum
typedef enum {
    #define X(code, message) code,
    ERROR_TABLE
    #undef X
    ERROR_COUNT
} ErrorCode;

// Generate string array
const char* error_messages[] = {
    #define X(code, message) message,
    ERROR_TABLE
    #undef X
};

const char* get_error_message(ErrorCode code) {
    if (code >= 0 && code < ERROR_COUNT) {
        return error_messages[code];
    }
    return "Unknown error";
}

int main() {
    for (ErrorCode i = SUCCESS; i < ERROR_COUNT; i++) {
        printf("Error %d: %s\n", i, get_error_message(i));
    }
    return 0;
}
```

## 42. Advanced Debugging Techniques

### 42.1 Custom Assertions with Context
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define CUSTOM_ASSERT(condition, message, ...) \
    do { \
        if (!(condition)) { \
            fprintf(stderr, "Assertion failed: %s\n", #condition); \
            fprintf(stderr, "File: %s, Line: %d\n", __FILE__, __LINE__); \
            fprintf(stderr, "Message: " message "\n", ##__VA_ARGS__); \
            abort(); \
        } \
    } while(0)

#define ASSERT_NOT_NULL(ptr) \
    CUSTOM_ASSERT((ptr) != NULL, "Pointer " #ptr " is NULL")

#define ASSERT_IN_RANGE(value, min, max) \
    CUSTOM_ASSERT((value) >= (min) && (value) <= (max), \
                 "Value %d out of range [%d, %d]", value, min, max)

void process_data(int *data, int size) {
    ASSERT_NOT_NULL(data);
    ASSERT_IN_RANGE(size, 1, 1000);
    
    for (int i = 0; i < size; i++) {
        ASSERT_IN_RANGE(data[i], 0, 100);
        // Process data
        data[i] *= 2;
    }
}

int main() {
    int valid_data[] = {10, 20, 30};
    process_data(valid_data, 3);
    
    // This will trigger assertion
    // int invalid_data[] = {10, 200, 30};
    // process_data(invalid_data, 3);
    
    printf("All assertions passed!\n");
    return 0;
}
```

## 43. Cross-Platform Development

### 43.1 Platform Detection
```c
#include <stdio.h>

// Platform detection
#if defined(_WIN32) || defined(_WIN64)
    #define PLATFORM_WINDOWS 1
    #ifdef _WIN64
        #define PLATFORM_WINDOWS_64 1
    #else
        #define PLATFORM_WINDOWS_32 1
    #endif
#elif defined(__linux__)
    #define PLATFORM_LINUX 1
#elif defined(__APPLE__) && defined(__MACH__)
    #define PLATFORM_MACOS 1
#elif defined(__unix__)
    #define PLATFORM_UNIX 1
#else
    #define PLATFORM_UNKNOWN 1
#endif

// Platform-specific code
void platform_specific_function() {
    #ifdef PLATFORM_WINDOWS
        printf("Running on Windows\n");
        // Windows-specific code
    #elif defined(PLATFORM_LINUX)
        printf("Running on Linux\n");
        // Linux-specific code
    #elif defined(PLATFORM_MACOS)
        printf("Running on macOS\n");
        // macOS-specific code
    #else
        printf("Running on unknown platform\n");
    #endif
}

// Endianness detection
int is_little_endian() {
    unsigned int x = 1;
    return *(char*)&x == 1;
}

int main() {
    platform_specific_function();
    
    if (is_little_endian()) {
        printf("Little-endian architecture\n");
    } else {
        printf("Big-endian architecture\n");
    }
    
    return 0;
}
```

## 44. Advanced Build Systems and Tooling

### 44.1 Makefile for Complex Projects
```makefile
# Advanced Makefile example
CC = gcc
CFLAGS = -Wall -Wextra -std=c11 -O2 -g
LDFLAGS = -lm -lpthread

# Source directories
SRC_DIR = src
OBJ_DIR = obj
BIN_DIR = bin

# Automatic dependency generation
DEPFLAGS = -MT $@ -MMD -MP -MF $(OBJ_DIR)/$*.d

# Source files
SOURCES = $(wildcard $(SRC_DIR)/*.c)
OBJECTS = $(SOURCES:$(SRC_DIR)/%.c=$(OBJ_DIR)/%.o)
DEPENDS = $(OBJECTS:.o=.d)

# Targets
TARGET = $(BIN_DIR)/program

# Phony targets
.PHONY: all clean debug release

all: $(TARGET)

# Include dependencies
-include $(DEPENDS)

# Main target
$(TARGET): $(OBJECTS) | $(BIN_DIR)
	$(CC) $(OBJECTS) -o $@ $(LDFLAGS)

# Object files
$(OBJ_DIR)/%.o: $(SRC_DIR)/%.c | $(OBJ_DIR)
	$(CC) $(CFLAGS) $(DEPFLAGS) -c $< -o $@

# Create directories
$(BIN_DIR) $(OBJ_DIR):
	mkdir -p $@

# Debug build
debug: CFLAGS += -DDEBUG -O0 -fsanitize=address
debug: all

# Release build
release: CFLAGS += -DNDEBUG -O3
release: all

# Clean
clean:
	rm -rf $(OBJ_DIR) $(BIN_DIR)

# Install (example)
install: all
	cp $(TARGET) /usr/local/bin/

# Run tests
test: all
	./$(TARGET) --test
```

## 45. Real-time Systems Programming

### 45.1 Real-time Constraints
```c
#include <stdio.h>
#include <time.h>
#include <sched.h>
#include <sys/mman.h>

void set_real_time_priority() {
    struct sched_param param;
    
    // Lock memory to prevent paging
    mlockall(MCL_CURRENT | MCL_FUTURE);
    
    // Set real-time scheduling policy
    param.sched_priority = sched_get_priority_max(SCHED_FIFO);
    if (sched_setscheduler(0, SCHED_FIFO, &param) == -1) {
        perror("sched_setscheduler");
    }
}

void real_time_delay_ns(long ns) {
    struct timespec req, rem;
    req.tv_sec = 0;
    req.tv_nsec = ns;
    
    // High-precision sleep
    while (nanosleep(&req, &rem) == -1) {
        req = rem;
    }
}

void real_time_task() {
    struct timespec start, end;
    long total_delay = 0;
    const int iterations = 1000;
    
    set_real_time_priority();
    
    for (int i = 0; i < iterations; i++) {
        clock_gettime(CLOCK_MONOTONIC, &start);
        
        // Real-time work
        for (volatile int j = 0; j < 1000; j++) {}
        
        // Precise 1ms delay
        real_time_delay_ns(1000000);  // 1ms
        
        clock_gettime(CLOCK_MONOTONIC, &end);
        
        long delay_ns = (end.tv_sec - start.tv_sec) * 1000000000L + 
                       (end.tv_nsec - start.tv_nsec);
        total_delay += labs(delay_ns - 1000000L);  // Deviation from 1ms
    }
    
    printf("Average timing deviation: %.2f microseconds\n", 
           (double)total_delay / iterations / 1000.0);
}

int main() {
    real_time_task();
    return 0;
}
```

