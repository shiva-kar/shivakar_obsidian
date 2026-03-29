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
- Store multiple strings of same maximum length
- Each string must end with null character `\0`
- Fixed width defined by column size
- Access: `charArray[row]` for string, `charArray[row][col]` for character

## 10 strings

## 10. Strings

## character handling functions 2

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

## string manipulation basics 2

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

