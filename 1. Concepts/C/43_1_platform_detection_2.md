### 43.1 Platform Detection
```c
#include <stdio.h>

// Platform detection
#if defined(_WIN32) || defined(_WIN64)
    #define PLATFORM_WINDOWS 1
    #ifdef _WIN64
        #define PLATFORM_WINDOWS_64 1
    #else
        #define PLATFORM_WINDOWS_32 1
    #endif
#elif defined(__linux__)
    #define PLATFORM_LINUX 1
#elif defined(__APPLE__) && defined(__MACH__)
    #define PLATFORM_MACOS 1
#elif defined(__unix__)
    #define PLATFORM_UNIX 1
#else
    #define PLATFORM_UNKNOWN 1
#endif

// Platform-specific code
void platform_specific_function() {
    #ifdef PLATFORM_WINDOWS
        printf("Running on Windows\n");
        // Windows-specific code
    #elif defined(PLATFORM_LINUX)
        printf("Running on Linux\n");
        // Linux-specific code
    #elif defined(PLATFORM_MACOS)
        printf("Running on macOS\n");
        // macOS-specific code
    #else
        printf("Running on unknown platform\n");
    #endif
}

// Endianness detection
int is_little_endian() {
    unsigned int x = 1;
    return *(char*)&x == 1;
}

int main() {
    platform_specific_function();
    
    if (is_little_endian()) {
        printf("Little-endian architecture\n");
    } else {
        printf("Big-endian architecture\n");
    }
    
    return 0;
}
```