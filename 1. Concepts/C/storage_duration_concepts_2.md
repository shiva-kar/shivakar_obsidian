###  **Storage Duration Concepts**

####  Automatic vs Static Duration
```c
#include <stdio.h>

void test_storage_duration() {
    int auto_var = 0;        // Automatic storage duration
    static int static_var = 0; // Static storage duration
    
    auto_var++;
    static_var++;
    
    printf("auto_var: %d, static_var: %d\n", auto_var, static_var);
}

int main() {
    printf("First call:\n");
    test_storage_duration();
    
    printf("Second call:\n");
    test_storage_duration();
    
    printf("Third call:\n");
    test_storage_duration();
    
    return 0;
}
```