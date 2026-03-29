# Memory Management

## Core Idea
Control allocation, lifetime, and release of memory safely.

## Why it exists
Essential for performance and correctness in non-GC languages.

## Mental Model
Own memory lifecycle: allocate -> use -> free exactly once.

## Code Pattern
~~~c
int *buf = malloc(10 * sizeof(int));
if (!buf) return 1;
/* use buf */
free(buf); buf = NULL;
~~~

## Common Mistakes
- Memory leak
- Double free / dangling pointer

## Interview Angle
- malloc vs calloc vs realloc
- Ownership and lifetime questions

## Related
- [[pointers]]
- [[arrays]]
- [[structs]]

## Legacy Notes (archived)
# memory management

Merged from legacy micro-notes.

## 12 1 what is dynamic memory allocation 2

### 12.1 What is Dynamic Memory Allocation
1. **Flexibility**: Allocate memory at runtime as needed
2. **Efficiency**: Use only necessary memory, release when done
3. **Persistence**: Memory persists beyond creation scope until freed
4. **Large Data**: Handle datasets exceeding stack size
5. **Data Structures**: Essential for linked lists, trees, graphs

## 12 2 using malloc 2

### 12.2 Using malloc
- Include `stdlib.h` header
- Pass size in bytes to allocate
- Cast returned `void*` to appropriate type
- Check for `NULL` (allocation failure)
- Does not initialize memory (may contain garbage)

## 12 3 using calloc 2

### 12.3 Using calloc
- Initializes all allocated memory to zero
- Takes two arguments: number of elements, element size
- Preferred for array allocation with zero-initialization
- Slightly more overhead than malloc
- Returns `void*` pointer (should be cast)

## 12 4 using free 2

### 12.4 Using free
- Deallocates previously allocated memory
- Essential for preventing memory leaks
- Takes pointer to allocated memory block
- Safe to call with `NULL` pointer (no operation)
- Pointer should not be used after freeing

## 12 5 using realloc 2

### 12.5 Using realloc
- Resizes previously allocated memory
- Preserves existing data when possible
- If passed `NULL`, behaves like `malloc`
- If size is 0, behaves like `free`
- Returns new pointer (may differ from original)
- Check return value before use

## 12 dynamic memory
