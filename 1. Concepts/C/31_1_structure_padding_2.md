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