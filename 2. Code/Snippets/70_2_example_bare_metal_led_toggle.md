### 70.2 Example: Bare-metal LED toggle

```cpp
#include <stdint.h>
#define LED_PORT *((volatile uint32_t*)0x40021018)

int main() {
    while (1) {
        LED_PORT ^= 1;  // toggle LED
        for (volatile int i = 0; i < 100000; ++i);
    }
}
```