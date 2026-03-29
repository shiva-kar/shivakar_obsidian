### 14.4 Conditional Compilation
```c
#ifdef DEBUG
    printf("Debug: x = %d\n", x);
#endif

#ifndef VERSION
    #define VERSION "1.0"
#endif

#if LEVEL == 1
    // Code for level 1
#elif LEVEL == 2
    // Code for level 2
#else
    // Default code
#endif
```