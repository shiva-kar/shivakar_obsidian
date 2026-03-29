### 34.1 Compiler Sanitizers
```c
// Compile with: gcc -fsanitize=address -fsanitize=undefined program.c

#include <stdio.h>
#include <stdlib.h>

void memory_errors() {
    // Buffer overflow
    int buffer[10];
    buffer[15] = 42;  // ASan will catch this
    
    // Use after free
    int *ptr = malloc(sizeof(int));
    free(ptr);
    *ptr = 10;  // ASan will catch this
    
    // Integer overflow
    int a = INT_MAX;
    a++;  // UBSan will catch this
}

int main() {
    memory_errors();
    return 0;
}
```