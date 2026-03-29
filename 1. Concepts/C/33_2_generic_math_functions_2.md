### 33.2 Generic Math Functions
```c
#include <stdio.h>
#include <math.h>

#define SQUARE(x) _Generic((x), \
    int: square_int, \
    double: square_double, \
    float: square_float \
)(x)

int square_int(int x) { return x * x; }
double square_double(double x) { return x * x; }
float square_float(float x) { return x * x; }

int main() {
    printf("Square of 5: %d\n", SQUARE(5));
    printf("Square of 2.5: %.2f\n", SQUARE(2.5));
    printf("Square of 1.5f: %.2f\n", SQUARE(1.5f));
    
    return 0;
}
```