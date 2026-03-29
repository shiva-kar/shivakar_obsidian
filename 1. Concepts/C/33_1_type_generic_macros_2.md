### 33.1 Type-Generic Macros
```c
#include <stdio.h>

#define print_value(x) _Generic((x), \
    int: print_int, \
    double: print_double, \
    char*: print_string, \
    default: print_unknown \
)(x)

void print_int(int x) {
    printf("Integer: %d\n", x);
}

void print_double(double x) {
    printf("Double: %.2f\n", x);
}

void print_string(char* x) {
    printf("String: %s\n", x);
}

void print_unknown() {
    printf("Unknown type\n");
}

int main() {
    print_value(42);
    print_value(3.14159);
    print_value("Hello World");
    
    return 0;
}
```