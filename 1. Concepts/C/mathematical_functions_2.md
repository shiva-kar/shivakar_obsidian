###  **Mathematical Functions**

####  math.h Basics
```c
#include <stdio.h>
#include <math.h>

int main() {
    double x = 2.5, y = 3.0;
    
    printf("sqrt(%.2f) = %.2f\n", x, sqrt(x));
    printf("pow(%.2f, %.2f) = %.2f\n", x, y, pow(x, y));
    printf("sin(%.2f) = %.2f\n", x, sin(x));
    printf("cos(%.2f) = %.2f\n", x, cos(x));
    printf("log(%.2f) = %.2f\n", x, log(x));
    printf("exp(%.2f) = %.2f\n", x, exp(x));
    printf("ceil(%.2f) = %.2f\n", x, ceil(x));
    printf("floor(%.2f) = %.2f\n", x, floor(x));
    printf("fabs(%.2f) = %.2f\n", -x, fabs(-x));
    
    return 0;
}
```