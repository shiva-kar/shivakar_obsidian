### 23.3 restrict Qualifier (C99)
```c
#include <stdio.h>

// restrict indicates pointers don't alias
void copyArray(int n, int *restrict dest, const int *restrict src) {
    for (int i = 0; i < n; i++) {
        dest[i] = src[i];  // Compiler can optimize better
    }
}

int main() {
    int src[] = {1, 2, 3, 4, 5};
    int dest[5];
    
    copyArray(5, dest, src);
    
    for (int i = 0; i < 5; i++) {
        printf("%d ", dest[i]);
    }
    printf("\n");
    
    return 0;
}
```