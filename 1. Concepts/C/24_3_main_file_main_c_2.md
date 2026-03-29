### 24.3 Main File (main.c)
```c
#include <stdio.h>
#include "math_utils.h"

int main() {
    int x = 10, y = 5;
    
    printf("%d + %d = %d\n", x, y, add(x, y));
    printf("%d - %d = %d\n", x, y, subtract(x, y));
    printf("%d * %d = %d\n", x, y, multiply(x, y));
    printf("%d / %d = %.2f\n", x, y, divide(x, y));
    printf("Square of %d: %d\n", x, square(x));
    printf("PI: %.5f\n", PI);
    
    return 0;
}
```