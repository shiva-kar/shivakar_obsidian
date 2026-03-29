### 32.2 Memory Ordering
```c
#include <stdatomic.h>
#include <stdio.h>

atomic_int data = ATOMIC_VAR_INIT(0);
atomic_int flag = ATOMIC_VAR_INIT(0);

void producer() {
    atomic_store_explicit(&data, 42, memory_order_relaxed);
    atomic_store_explicit(&flag, 1, memory_order_release);
}

void consumer() {
    while (atomic_load_explicit(&flag, memory_order_acquire) == 0) {
        // spin wait
    }
    int value = atomic_load_explicit(&data, memory_order_relaxed);
    printf("Consumed: %d\n", value);
}

int main() {
    producer();
    consumer();
    return 0;
}
```