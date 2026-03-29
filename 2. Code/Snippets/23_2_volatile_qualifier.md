### 23.2 volatile Qualifier
```c
#include <stdio.h>

volatile int hardware_register;

void readHardware() {
    // volatile tells compiler this value might change unexpectedly
    int value = hardware_register;
    // Compiler won't optimize away this read
}

int main() {
    // Simulate hardware changing the register
    for (int i = 0; i < 10; i++) {
        hardware_register = i;
        readHardware();
    }
    return 0;
}
```