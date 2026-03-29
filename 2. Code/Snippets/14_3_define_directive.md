### 14.3 `#define` Directive
**Macro Definitions:**
```c
#define PI 3.14159
#define MAX(a, b) ((a) > (b) ? (a) : (b))
#define SQUARE(x) ((x) * (x))
```

**Advantages:**
- No function call overhead
- Type-independent
- Compile-time evaluation

**Pitfalls:**
```c
#define SQUARE(x) x * x
SQUARE(5 + 3) // Expands to: 5 + 3 * 5 + 3 = 23 (not 64)
```