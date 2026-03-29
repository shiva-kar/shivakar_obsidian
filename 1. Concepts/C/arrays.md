# Arrays

## Core Idea
Arrays store same-type elements contiguously.

## Why it exists
They provide cache-friendly indexed access.

## Mental Model
Array = fixed-size contiguous block; index maps to offset.

## Code Pattern
~~~c
int arr[3] = {1,2,3};
for (int i = 0; i < 3; i++) printf("%d ", arr[i]);
~~~

## Common Mistakes
- Out-of-bounds access
- Confusing array decay in function parameters

## Interview Angle
- 2D array memory layout
- Time complexity of traversals

## Related
- [[pointers]]
- [[control_flow]]
- [[strings]]

## Legacy Notes (archived)
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

###


## Questions
- When should I use this instead of an alternative?
- What edge case is most likely to break this approach?

