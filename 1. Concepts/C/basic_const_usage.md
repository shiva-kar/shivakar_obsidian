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