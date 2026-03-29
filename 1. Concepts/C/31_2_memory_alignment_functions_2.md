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