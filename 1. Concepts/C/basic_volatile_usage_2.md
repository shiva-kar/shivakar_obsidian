### **Basic volatile Usage**

#### volatile Variables
```c
#include <stdio.h>
#include <signal.h>
#include <unistd.h>

volatile int flag = 0;

void handle_signal(int sig) {
    flag = 1;
}

int main() {
    signal(SIGINT, handle_signal);
    
    printf("Press Ctrl+C to set flag...\n");
    
    while (!flag) {
        // Without volatile, compiler might optimize this loop
        // With volatile, compiler always reads from memory
    }
    
    printf("Flag set! Exiting...\n");
    return 0;
}
```