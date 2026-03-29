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