### 12.2 Using malloc
- Include `stdlib.h` header
- Pass size in bytes to allocate
- Cast returned `void*` to appropriate type
- Check for `NULL` (allocation failure)
- Does not initialize memory (may contain garbage)