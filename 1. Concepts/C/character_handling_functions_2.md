### **Character Handling Functions**

####  ctype.h Functions
```c
#include <stdio.h>
#include <ctype.h>

int main() {
    char ch = 'A';
    
    printf("isalpha('%c'): %d\n", ch, isalpha(ch));
    printf("isdigit('%c'): %d\n", ch, isdigit(ch));
    printf("isupper('%c'): %d\n", ch, isupper(ch));
    printf("islower('%c'): %d\n", ch, islower(ch));
    printf("isspace('%c'): %d\n", ch, isspace(ch));
    
    // Conversion functions
    printf("tolower('%c'): %c\n", ch, tolower(ch));
    printf("toupper('%c'): %c\n", 'b', toupper('b'));
    
    return 0;
}
```