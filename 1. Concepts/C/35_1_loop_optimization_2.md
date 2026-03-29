### 35.1 Loop Optimization
```c
#include <stdio.h>
#include <time.h>

#define SIZE 1000000

void unoptimized_loop(int *arr) {
    for (int i = 0; i < SIZE; i++) {
        arr[i] = i * 2 + 1;
    }
}

void optimized_loop(int *arr) {
    int *end = arr + SIZE;
    int value = 1;
    
    // Loop unrolling and pointer arithmetic
    while (arr < end - 3) {
        *arr++ = value; value += 2;
        *arr++ = value; value += 2;
        *arr++ = value; value += 2;
        *arr++ = value; value += 2;
    }
    
    // Handle remaining elements
    while (arr < end) {
        *arr++ = value; value += 2;
    }
}

int main() {
    int arr1[SIZE], arr2[SIZE];
    clock_t start, end;
    
    start = clock();
    unoptimized_loop(arr1);
    end = clock();
    printf("Unoptimized: %.6f seconds\n", (double)(end - start) / CLOCKS_PER_SEC);
    
    start = clock();
    optimized_loop(arr2);
    end = clock();
    printf("Optimized: %.6f seconds\n", (double)(end - start) / CLOCKS_PER_SEC);
    
    return 0;
}
```