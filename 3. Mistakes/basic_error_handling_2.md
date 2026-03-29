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