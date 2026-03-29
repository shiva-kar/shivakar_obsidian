### 17.2 Union Declaration and Usage
```c
#include <stdio.h>

union Data {
    int i;
    float f;
    char str[20];
};

int main() {
    union Data data;
    
    printf("Memory size occupied by data: %lu\n", sizeof(data));
    
    data.i = 10;
    printf("data.i: %d\n", data.i);
    
    data.f = 220.5;
    printf("data.f: %.2f\n", data.f);
    
    // data.i is now corrupted because memory is shared
    printf("data.i after setting f: %d (corrupted)\n", data.i);
    
    return 0;
}
```