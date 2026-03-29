# arrays

Merged from legacy micro-notes.

## 20 1 vla declaration 2

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

## 20 variable length arrays vlas 2

## 20. Variable Length Arrays (VLAs)

## 9 1 need of array 2

### 9.1 Need of Array
- List of values
- Index starts with 0
- Store multiple values in single variable
- Efficient data organization

## 9 10 two dimensional array 2

### 9.10 Two-Dimensional Array
- Array of arrays (matrices/grids)
- Declaration: `int arr[3][4];` (3 rows, 4 columns)
- Initialization: `int arr[2][2] = {{1, 2}, {3, 4}};`
- Access: `arr[row][column]`
- Row-major order storage

## 9 11 multi dimensional array 2

### 9.11 Multi-Dimensional Array
- Extension to more dimensions (3D+, cubes)
- Declaration: `int arr[2][3][4];` (3D array)
- Nested braces initialization
- Access: `arr[x][y][z]`
- Row-major order continues

## 9 2 array declaration

### 9.2 Array Declaration
- Syntax: `type name[size];` (e.g., `int arr[10];`)
- Fixed size (known at compile time)
- Zero-based indexing
- Contiguous memory block
- All elements same type

## 9 3 accessing array elements 2

### 9.3 Accessing Array Elements
- Use indexes: `arr[index]`
- Start at 0: `arr[0]` is first element
- Use loops for iteration
- No automatic bounds checking

## 9 4 array initialization 2

### 9.4 Array Initialization
- Direct: `int nums[] = {1, 2, 3};`
- Auto zero-fill: `int arr[5] = {1};` (others become 0)
- Zero array: `int arr[5] = {0};`
- Designated: `int arr[5] = {[2] = 5};`

## 9 5 array traversal 2

### 9.5 Array Traversal
- Orderly visit from start to end
- Use `for` or `while` loops
- Indexes: 0 to size-1
- Modify or read elements
- Pointer arithmetic option

## 9 6 bounds checking 2

### 9.6 Bounds Checking
- C doesn't auto-check array bounds
- Programmer must ensure valid indices
- Out-of-bounds access can cause crashes/security issues
- Always validate indices against array size

## 9 7 array as function arguments 2

### 9.7 Array as Function Arguments
- Arrays become pointers when passed to functions
- Call by reference (changes affect original)
- Pass array size as extra argument
- Specify element type in parameters
- Efficient (only pointer passed, no full copy)

## 9 8 pointer arithmetic 2

### 9.8 Pointer Arithmetic
- `*(arr + i)` equals `arr[i]`
- `ptr++` or `ptr--` moves pointer based on type size
- Adding/subtracting integers moves pointer by elements
- Pointer subtraction gives number of elements between

## 9 9 pointers and arrays 2

### 9.9 Pointers and Arrays
- Array name acts as constant pointer to first element
- Array decays to pointer when passed to functions
- Can access elements via pointer arithmetic

## 9 arrays 2

## 9. Arrays

