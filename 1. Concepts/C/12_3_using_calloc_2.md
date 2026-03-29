### 12.3 Using calloc
- Initializes all allocated memory to zero
- Takes two arguments: number of elements, element size
- Preferred for array allocation with zero-initialization
- Slightly more overhead than malloc
- Returns `void*` pointer (should be cast)