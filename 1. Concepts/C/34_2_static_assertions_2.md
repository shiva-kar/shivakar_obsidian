### 34.2 Static Assertions
```c
#include <stdio.h>
#include <assert.h>

// Compile-time assertions
static_assert(sizeof(int) == 4, "int must be 4 bytes");
static_assert(sizeof(long) >= 4, "long must be at least 4 bytes");

// Custom static assertion macro
#define STATIC_ASSERT(condition, message) \
    typedef char static_assert_##message[(condition) ? 1 : -1]

STATIC_ASSERT(sizeof(void*) == 8, "64_bit_required");

int main() {
    printf("All static assertions passed!\n");
    return 0;
}
```