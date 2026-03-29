# memory management

Merged from legacy micro-notes.

## 12 1 what is dynamic memory allocation 2

### 12.1 What is Dynamic Memory Allocation
1. **Flexibility**: Allocate memory at runtime as needed
2. **Efficiency**: Use only necessary memory, release when done
3. **Persistence**: Memory persists beyond creation scope until freed
4. **Large Data**: Handle datasets exceeding stack size
5. **Data Structures**: Essential for linked lists, trees, graphs

## 12 2 using malloc 2

### 12.2 Using malloc
- Include `stdlib.h` header
- Pass size in bytes to allocate
- Cast returned `void*` to appropriate type
- Check for `NULL` (allocation failure)
- Does not initialize memory (may contain garbage)

## 12 3 using calloc 2

### 12.3 Using calloc
- Initializes all allocated memory to zero
- Takes two arguments: number of elements, element size
- Preferred for array allocation with zero-initialization
- Slightly more overhead than malloc
- Returns `void*` pointer (should be cast)

## 12 4 using free 2

### 12.4 Using free
- Deallocates previously allocated memory
- Essential for preventing memory leaks
- Takes pointer to allocated memory block
- Safe to call with `NULL` pointer (no operation)
- Pointer should not be used after freeing

## 12 5 using realloc 2

### 12.5 Using realloc
- Resizes previously allocated memory
- Preserves existing data when possible
- If passed `NULL`, behaves like `malloc`
- If size is 0, behaves like `free`
- Returns new pointer (may differ from original)
- Check return value before use

## 12 dynamic memory allocation 2

## 12. Dynamic Memory Allocation

## 12 dynamic memory raii

## 12. Dynamic Memory & RAII

- Prefer RAII: resources owned by objects and freed in destructors
    
- Raw `new`/`delete` are legal but discouraged
    
- Use smart pointers (`std::unique_ptr`, `std::shared_ptr`, `std::weak_ptr`)
    
- `std::make_unique`, `std::make_shared`
    

```cpp
#include <memory>

auto p = std::make_unique<int>(42); // unique_ptr<int>
```

## 25 1 memory pool allocator 2

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

## 25 advanced memory management 2

## 25. Advanced Memory Management

## 25 function pointers std function callables

## 25. Function Pointers, std::function & Callables

- Function pointers exist
    
- `std::function` and `std::bind`, lambdas for higher-level callables
    

```cpp
#include <functional>
std::function<int(int,int)> op = [](int a,int b){ return a+b; };
```

## 31 1 structure padding 2

### 31.1 Structure Padding
```c
#include <stdio.h>

struct Unaligned {
    char a;     // 1 byte
    int b;      // 4 bytes
    char c;     // 1 byte
}; // Size: 12 bytes (not 6) due to padding

struct Aligned {
    int b;      // 4 bytes
    char a;     // 1 byte
    char c;     // 1 byte
}; // Size: 8 bytes (better packing)

#pragma pack(push, 1)
struct Packed {
    char a;
    int b;
    char c;
}; // Size: 6 bytes (no padding)
#pragma pack(pop)

int main() {
    printf("Unaligned size: %lu\n", sizeof(struct Unaligned));
    printf("Aligned size: %lu\n", sizeof(struct Aligned));
    printf("Packed size: %lu\n", sizeof(struct Packed));
    
    return 0;
}
```

## 31 2 memory alignment functions 2

### 31.2 Memory Alignment Functions
```c
#include <stdio.h>
#include <stdlib.h>
#include <stdalign.h>

int main() {
    // C11 alignment features
    printf("max_align_t alignment: %zu\n", alignof(max_align_t));
    printf("double alignment: %zu\n", alignof(double));
    
    // Aligned memory allocation
    int *aligned_ptr = aligned_alloc(16, 1024); // 16-byte aligned
    if (aligned_ptr) {
        printf("Aligned pointer: %p\n", (void*)aligned_ptr);
        free(aligned_ptr);
    }
    
    return 0;
}
```

## 31 memory alignment and padding 2

## 31. Memory Alignment and Padding

## 41 memory management deep dive

## 41. Memory Management Deep Dive

