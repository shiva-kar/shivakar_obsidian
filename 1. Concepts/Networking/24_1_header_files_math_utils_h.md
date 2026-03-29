### 24.1 Header Files (math_utils.h)
```c
#ifndef MATH_UTILS_H
#define MATH_UTILS_H

// Function declarations
int add(int a, int b);
int subtract(int a, int b);
int multiply(int a, int b);
double divide(int a, int b);

// Constant definitions
#define PI 3.14159
#define MAX_VALUE 100

// Inline function
static inline int square(int x) {
    return x * x;
}

#endif
```