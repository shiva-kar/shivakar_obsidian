### 21.1 Inline Function Definition
```c
#include <stdio.h>

// Inline function suggestion to compiler
static inline int max(int a, int b) {
    return (a > b) ? a : b;
}

static inline double square(double x) {
    return x * x;
}

int main() {
    int a = 10, b = 20;
    double x = 5.5;
    
    printf("Max of %d and %d: %d\n", a, b, max(a, b));
    printf("Square of %.2f: %.2f\n", x, square(x));
    
    return 0;
}
```