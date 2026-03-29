### 35.2 Branch Prediction Optimization
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define SIZE 1000000

// Data that's mostly sorted (good for branch prediction)
void process_sorted_data() {
    int data[SIZE];
    int sum = 0;
    
    // Create mostly sorted data with some randomness
    for (int i = 0; i < SIZE; i++) {
        data[i] = i + (rand() % 10 - 5);  // Mostly increasing
    }
    
    clock_t start = clock();
    for (int i = 0; i < SIZE - 1; i++) {
        if (data[i] < data[i + 1]) {  // Usually true - predictable
            sum += data[i];
        }
    }
    clock_t end = clock();
    printf("Sorted data time: %.6f seconds\n", (double)(end - start) / CLOCKS_PER_SEC);
}

// Data that's random (bad for branch prediction)
void process_random_data() {
    int data[SIZE];
    int sum = 0;
    
    // Create random data
    for (int i = 0; i < SIZE; i++) {
        data[i] = rand() % 1000;
    }
    
    clock_t start = clock();
    for (int i = 0; i < SIZE - 1; i++) {
        if (data[i] < data[i + 1]) {  // 50/50 chance - unpredictable
            sum += data[i];
        }
    }
    clock_t end = clock();
    printf("Random data time: %.6f seconds\n", (double)(end - start) / CLOCKS_PER_SEC);
}

int main() {
    srand(time(NULL));
    process_sorted_data();
    process_random_data();
    return 0;
}
```