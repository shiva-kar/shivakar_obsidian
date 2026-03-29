### 25.1 Memory Pool Allocator
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define POOL_SIZE 1024

typedef struct {
    char pool[POOL_SIZE];
    size_t used;
} MemoryPool;

void* pool_alloc(MemoryPool *pool, size_t size) {
    if (pool->used + size > POOL_SIZE) {
        return NULL;  // Out of memory
    }
    
    void *ptr = pool->pool + pool->used;
    pool->used += size;
    return ptr;
}

void pool_reset(MemoryPool *pool) {
    pool->used = 0;
}

int main() {
    MemoryPool pool = {0};
    
    int *numbers = pool_alloc(&pool, 10 * sizeof(int));
    char *text = pool_alloc(&pool, 100 * sizeof(char));
    
    if (numbers && text) {
        for (int i = 0; i < 10; i++) {
            numbers[i] = i * i;
        }
        
        strcpy(text, "Hello from memory pool!");
        
        printf("Numbers: ");
        for (int i = 0; i < 10; i++) {
            printf("%d ", numbers[i]);
        }
        printf("\nText: %s\n", text);
    }
    
    pool_reset(&pool);  // Reset for reuse
    
    return 0;
}
```