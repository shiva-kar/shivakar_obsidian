### 36.2 Interrupt Service Routines
```c
#include <stdint.h>

// Interrupt vector table (simplified)
typedef void (*isr_function_t)(void);

// ISR function attributes (compiler-specific)
#define ISR __attribute__((interrupt))

// Example ISRs
ISR void systick_handler(void) {
    // System tick timer interrupt
    static uint32_t ticks = 0;
    ticks++;
    
    // Toggle LED every 1000 ticks
    if (ticks % 1000 == 0) {
        TOGGLE_BIT(GPIO_ODR, 5);  // Toggle LED pin
    }
}

ISR void uart_receive_handler(void) {
    // UART receive interrupt
    uint8_t data = UART_DR;  // Read received data
    
    // Echo back
    UART_DR = data;
}

// Interrupt vector table
isr_function_t vector_table[] __attribute__((section(".isr_vector"))) = {
    (isr_function_t)0x20001000,  // Initial stack pointer
    NULL,                        // Reset handler
    systick_handler,             // System tick timer
    uart_receive_handler,        // UART receive
    // ... more ISRs
};
```