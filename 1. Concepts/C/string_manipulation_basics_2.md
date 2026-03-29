###  **String Manipulation Basics**

####  Basic String Functions
```c
#include <stdio.h>
#include <string.h>

int main() {
    char str1[20] = "Hello";
    char str2[20] = "World";
    char str3[40];
    
    // String length
    printf("Length of '%s': %zu\n", str1, strlen(str1));
    
    // String copy
    strcpy(str3, str1);
    printf("After strcpy: %s\n", str3);
    
    // String concatenation
    strcat(str3, " ");
    strcat(str3, str2);
    printf("After strcat: %s\n", str3);
    
    // String comparison
    int cmp = strcmp(str1, str2);
    if (cmp < 0) {
        printf("'%s' comes before '%s'\n", str1, str2);
    } else if (cmp > 0) {
        printf("'%s' comes after '%s'\n", str1, str2);
    } else {
        printf("Strings are equal\n");
    }
    
    // String search
    char *found = strchr(str3, 'W');
    if (found) {
        printf("Found 'W' at position: %ld\n", found - str3);
    }
    
    return 0;
}
```