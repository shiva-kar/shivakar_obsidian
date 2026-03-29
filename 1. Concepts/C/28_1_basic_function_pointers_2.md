### 28.1 Basic Function Pointers
```c
#include <stdio.h>

int add(int a, int b) {
    return a + b;
}

int subtract(int a, int b) {
    return a - b;
}

int multiply(int a, int b) {
    return a * b;
}

int divide(int a, int b) {
    return b != 0 ? a / b : 0;
}

int main() {
    // Function pointer declaration
    int (*operation)(int, int);
    
    int x = 10, y = 5;
    
    // Use function pointer
    operation = add;
    printf("%d + %d = %d\n", x, y, operation(x, y));
    
    operation = subtract;
    printf("%d - %d = %d\n", x, y, operation(x, y));
    
    operation = multiply;
    printf("%d * %d = %d\n", x, y, operation(x, y));
    
    operation = divide;
    printf("%d / %d = %d\n", x, y, operation(x, y));
    
    return 0;
}
```