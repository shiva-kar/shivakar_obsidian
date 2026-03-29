### 32.1 Atomic Variables
```c
#include <stdio.h>
#include <stdatomic.h>
#include <threads.h>

atomic_int counter = ATOMIC_VAR_INIT(0);

int increment_thread(void *arg) {
    for (int i = 0; i < 100000; i++) {
        atomic_fetch_add(&counter, 1);
    }
    return 0;
}

int main() {
    thrd_t t1, t2;
    
    thrd_create(&t1, increment_thread, NULL);
    thrd_create(&t2, increment_thread, NULL);
    
    thrd_join(t1, NULL);
    thrd_join(t2, NULL);
    
    printf("Final counter value: %d\n", atomic_load(&counter));
    printf("Expected: 200000\n");
    
    return 0;
}
```