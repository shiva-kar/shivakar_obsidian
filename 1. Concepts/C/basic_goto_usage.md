### **Basic goto Usage**

####  goto for Error Handling
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    FILE *file1 = NULL, *file2 = NULL;
    
    file1 = fopen("file1.txt", "r");
    if (file1 == NULL) {
        goto cleanup;
    }
    
    file2 = fopen("file2.txt", "w");
    if (file2 == NULL) {
        goto cleanup;
    }
    
    // Process files...
    printf("Files opened successfully\n");
    
cleanup:
    if (file1) fclose(file1);
    if (file2) fclose(file2);
    
    return 0;
}
```