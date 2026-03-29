### 42.1 Custom Assertions with Context
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define CUSTOM_ASSERT(condition, message, ...) \
    do { \
        if (!(condition)) { \
            fprintf(stderr, "Assertion failed: %s\n", #condition); \
            fprintf(stderr, "File: %s, Line: %d\n", __FILE__, __LINE__); \
            fprintf(stderr, "Message: " message "\n", ##__VA_ARGS__); \
            abort(); \
        } \
    } while(0)

#define ASSERT_NOT_NULL(ptr) \
    CUSTOM_ASSERT((ptr) != NULL, "Pointer " #ptr " is NULL")

#define ASSERT_IN_RANGE(value, min, max) \
    CUSTOM_ASSERT((value) >= (min) && (value) <= (max), \
                 "Value %d out of range [%d, %d]", value, min, max)

void process_data(int *data, int size) {
    ASSERT_NOT_NULL(data);
    ASSERT_IN_RANGE(size, 1, 1000);
    
    for (int i = 0; i < size; i++) {
        ASSERT_IN_RANGE(data[i], 0, 100);
        // Process data
        data[i] *= 2;
    }
}

int main() {
    int valid_data[] = {10, 20, 30};
    process_data(valid_data, 3);
    
    // This will trigger assertion
    // int invalid_data[] = {10, 200, 30};
    // process_data(invalid_data, 3);
    
    printf("All assertions passed!\n");
    return 0;
}
```