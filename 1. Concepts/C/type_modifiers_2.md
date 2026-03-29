###  **Type Modifiers**

####  signed and unsigned
```c
#include <stdio.h>
#include <limits.h>

int main() {
    signed int s_int = -100;
    unsigned int u_int = 100;
    
    printf("Signed int range: %d to %d\n", INT_MIN, INT_MAX);
    printf("Unsigned int range: 0 to %u\n", UINT_MAX);
    
    // Be careful with mixing signed and unsigned
    int signed_val = -5;
    unsigned int unsigned_val = 10;
    
    if (signed_val < unsigned_val) {
        printf("This might not work as expected!\n");
    }
    
    return 0;
}
```

####  short and long
```c
#include <stdio.h>

int main() {
    short small_number = 32767;  // Typically 2 bytes
    int normal_number = 2147483647;  // Typically 4 bytes
    long large_number = 2147483647L;  // Typically 4 or 8 bytes
    long long very_large = 9223372036854775807LL;  // Typically 8 bytes
    
    printf("short: %hd, size: %zu bytes\n", small_number, sizeof(short));
    printf("int: %d, size: %zu bytes\n", normal_number, sizeof(int));
    printf("long: %ld, size: %zu bytes\n", large_number, sizeof(long));
    printf("long long: %lld, size: %zu bytes\n", very_large, sizeof(long long));
    
    return 0;
}
```