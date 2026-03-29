### 12.4 Using free
- Deallocates previously allocated memory
- Essential for preventing memory leaks
- Takes pointer to allocated memory block
- Safe to call with `NULL` pointer (no operation)
- Pointer should not be used after freeing