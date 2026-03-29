### **Basic setjmp/longjmp**

####  Non-local Jumps
```c
#include <stdio.h>
#include <setjmp.h>
#include <stdlib.h>

jmp_buf env;

void function_b() {
    printf("In function_b\n");
    longjmp(env, 1);  // Jump back to setjmp point
    printf("This won't be printed\n");
}

void function_a() {
    printf("In function_a\n");
    function_b();
    printf("This won't be printed either\n");
}

int main() {
    if (setjmp(env) == 0) {
        printf("First time through\n");
        function_a();
    } else {
        printf("After longjmp\n");
    }
    
    return 0;
}
```