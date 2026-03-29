# Strings

## Core Idea
C strings are char arrays terminated by null character.

## Why it exists
Text processing in C depends on correct null termination and bounds checks.

## Mental Model
String = array of chars ending with `\\0`.

## Code Pattern
~~~c
char name[16] = "Shiva";
printf("%s\\n", name);
~~~

## Common Mistakes
- Missing null terminator
- Buffer overflow via unsafe copy/read

## Interview Angle
- fgets vs scanf for input
- Common string API pitfalls

## Related
- [[arrays]]
- [[file_io]]
- [[memory_management]]

## Legacy Notes (archived)
# strings

Merged from legacy micro-notes.

## 10 1 what is a string 2

### 10.1 What is a String
- Sequence of characters terminated by null character `\0`
- Null character marks end (not included in length)
- String literals in double quotes: `"Hello, World!"`
- Mutable when stored in character arrays

## 10 2 string memory allocation

### 10.2 String Memory Allocation
- Fixed size at compile time (includes null terminator)
- Contiguous memory storage like arrays
- Pre-allocated memory blocks

## 10 4 format specifiers 2

### 10.4 Format Specifiers
- Output: `%s` with `printf`
- Input: `%s` with `scanf` (stops at whitespace/newline/EOF)
- No `&` with `scanf` for strings (array name acts as pointer)
- Safety: Specify field width (e.g., `%49s` for 50-char array)

## 10 5 fgets and puts functions

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

## 10 6 pointers and strings 2

### 10.6 Pointers and Strings
- String represented as pointer to first character
- Example: `char *str = "Hello";`
- String literals immutable when assigned to pointers
- Character arrays allow modification

## 10 8 2 d array of characters

### 10.8 2-D Array of Characters
- Matrix where each row represents a string
- Store multi


## Questions
- When should I use this instead of an alternative?
- What edge case is most likely to break this approach?

