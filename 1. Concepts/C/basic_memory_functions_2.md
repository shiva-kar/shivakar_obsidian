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