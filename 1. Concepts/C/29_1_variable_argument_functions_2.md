### 29.1 Variable Argument Functions
```c
#include <stdio.h>
#include <stdarg.h>

// Simple variadic function
int sum(int count, ...) {
    va_list args;
    va_start(args, count);
    
    int total = 0;
    for (int i = 0; i < count; i++) {
        total += va_arg(args, int);
    }
    
    va_end(args);
    return total;
}

// Variadic function with format string
void printValues(const char *format, ...) {
    va_list args;
    va_start(args, format);
    
    while (*format) {
        switch (*format) {
            case 'd':
                printf("%d ", va_arg(args, int));
                break;
            case 'f':
                printf("%.2f ", va_arg(args, double));
                break;
            case 'c':
                printf("%c ", va_arg(args, int));  // char promoted to int
                break;
            case 's':
                printf("%s ", va_arg(args, char*));
                break;
        }
        format++;
    }
    printf("\n");
    
    va_end(args);
}

int main() {
    printf("Sum of 3 numbers: %d\n", sum(3, 10, 20, 30));
    printf("Sum of 5 numbers: %d\n", sum(5, 1, 2, 3, 4, 5));
    
    printValues("dfs", 42, 3.14159, "Hello");
    printValues("cccd", 'A', 'B', 'C', 100);
    
    return 0;
}
```