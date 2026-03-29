### 17.3 Practical Use Case: Variant Type
```c
#include <stdio.h>

typedef enum { INT, FLOAT, CHAR } Type;

typedef struct {
    Type type;
    union {
        int i;
        float f;
        char c;
    } value;
} Variant;

void printVariant(Variant v) {
    switch (v.type) {
        case INT:
            printf("Integer: %d\n", v.value.i);
            break;
        case FLOAT:
            printf("Float: %.2f\n", v.value.f);
            break;
        case CHAR:
            printf("Char: %c\n", v.value.c);
            break;
    }
}

int main() {
    Variant v1 = {INT, {.i = 10}};
    Variant v2 = {FLOAT, {.f = 3.14}};
    Variant v3 = {CHAR, {.c = 'A'}};
    
    printVariant(v1);
    printVariant(v2);
    printVariant(v3);
    
    return 0;
}
```