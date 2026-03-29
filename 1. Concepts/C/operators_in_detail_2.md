### **Operators in Detail**
####  Comma Operator
```c
#include <stdio.h>

int main() {
    int a, b, c;
    
    // Comma operator example
    a = (b = 3, c = 4, b + c); // a gets 7
    printf("a = %d, b = %d, c = %d\n", a, b, c);
    
    // In for loops
    for (int i = 0, j = 10; i < j; i++, j--) {
        printf("i = %d, j = %d\n", i, j);
    }
    
    return 0;
}
```

####  sizeof Operator
```c
#include <stdio.h>

int main() {
    int arr[10];
    
    printf("Size of int: %zu bytes\n", sizeof(int));
    printf("Size of array: %zu bytes\n", sizeof(arr));
    printf("Number of elements: %zu\n", sizeof(arr) / sizeof(arr[0]));
    
    // sizeof with expressions
    int x = 5;
    printf("Size of expression: %zu\n", sizeof(x + 3.14));
    
    return 0;
}
```

#### Conditional Operator
```c
#include <stdio.h>

int main() {
    int a = 10, b = 20;
    
    // Basic conditional operator
    int max = (a > b) ? a : b;
    printf("Maximum: %d\n", max);
    
    // Nested conditional operator
    int num = -5;
    char* result = (num > 0) ? "Positive" : (num < 0) ? "Negative" : "Zero";
    printf("Number is: %s\n", result);
    
    return 0;
}
```