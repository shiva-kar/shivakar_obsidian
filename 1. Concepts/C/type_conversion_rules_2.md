###  **Type Conversion Rules**

####  Implicit Type Conversion
```c
#include <stdio.h>

int main() {
    // Integer promotion
    char c1 = 100, c2 = 100;
    int result = c1 * c2;  // chars promoted to int
    printf("char * char = int: %d\n", result);
    
    // Usual arithmetic conversions
    int i = 10;
    float f = 3.14;
    double d = i + f;  // i converted to float, then to double
    printf("int + float = double: %.2f\n", d);
    
    // Sign extension
    signed char sc = -10;
    unsigned char uc = 200;
    int signed_extended = sc;    // Sign extended
    int unsigned_extended = uc;  // Zero extended
    printf("Signed char extended: %d\n", signed_extended);
    printf("Unsigned char extended: %d\n", unsigned_extended);
    
    return 0;
}
```