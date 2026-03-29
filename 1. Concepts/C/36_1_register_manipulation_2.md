### 36.1 Register Manipulation
```c
#include <stdint.h>

// Memory-mapped registers (typical in embedded systems)
#define GPIO_BASE 0x40020000UL
#define GPIO_MODER (*(volatile uint32_t*)(GPIO_BASE + 0x00))
#define GPIO_OTYPER (*(volatile uint32_t*)(GPIO_BASE + 0x04))
#define GPIO_OSPEEDR (*(volatile uint32_t*)(GPIO_BASE + 0x08))

// Bit manipulation macros
#define SET_BIT(reg, bit) ((reg) |= (1UL << (bit)))
#define CLEAR_BIT(reg, bit) ((reg) &= ~(1UL << (bit)))
#define TOGGLE_BIT(reg, bit) ((reg) ^= (1UL << (bit)))
#define READ_BIT(reg, bit) (((reg) >> (bit)) & 1UL)

void configure_led_pin() {
    // Set pin 5 as output (bits 10-11 in MODER register)
    CLEAR_BIT(GPIO_MODER, 11);
    SET_BIT(GPIO_MODER, 10);
    
    // Set output type to push-pull (bit 5 in OTYPER)
    CLEAR_BIT(GPIO_OTYPER, 5);
    
    // Set medium speed (bits 10-11 in OSPEEDR)
    SET_BIT(GPIO_OSPEEDR, 10);
    CLEAR_BIT(GPIO_OSPEEDR, 11);
}
```