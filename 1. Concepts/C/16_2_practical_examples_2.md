### 16.2 Practical Examples
```c
#include <stdio.h>

void printBinary(unsigned int num) {
    for (int i = 31; i >= 0; i--) {
        printf("%d", (num >> i) & 1);
        if (i % 8 == 0) printf(" ");
    }
    printf("\n");
}

int main() {
    unsigned int a = 5;    // 00000101
    unsigned int b = 3;    // 00000011
    
    printf("a & b  = "); printBinary(a & b);   // AND: 00000001 (1)
    printf("a | b  = "); printBinary(a | b);   // OR:  00000111 (7)
    printf("a ^ b  = "); printBinary(a ^ b);   // XOR: 00000110 (6)
    printf("~a     = "); printBinary(~a);      // NOT: 11111010 (large number)
    printf("a << 1 = "); printBinary(a << 1);  // Left shift: 00001010 (10)
    printf("a >> 1 = "); printBinary(a >> 1);  // Right shift: 00000010 (2)
    
    return 0;
}
```