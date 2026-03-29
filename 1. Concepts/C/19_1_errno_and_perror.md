### 19.1 errno and perror
```c
#include <stdio.h>
#include <errno.h>
#include <string.h>

int main() {
    FILE *file = fopen("nonexistent.txt", "r");
    
    if (file == NULL) {
        printf("Error number: %d\n", errno);
        perror("Error message");
        printf("Error description: %s\n", strerror(errno));
    }
    
    return 0;
}
```