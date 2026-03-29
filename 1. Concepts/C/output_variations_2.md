### **Basic Input/Output Variations**

#### Character I/O
```c
#include <stdio.h>

int main() {
    char ch;
    
    printf("Enter a character: ");
    ch = getchar();  // Read single character
    printf("You entered: ");
    putchar(ch);     // Write single character
    putchar('\n');
    
    // Using getc and putc
    printf("Enter another character: ");
    ch = getc(stdin);
    printf("You entered: ");
    putc(ch, stdout);
    putc('\n', stdout);
    
    return 0;
}
```

####  String I/O
```c
#include <stdio.h>

int main() {
    char name[50];
    
    printf("Enter your name: ");
    fgets(name, sizeof(name), stdin);  // Safe string input
    
    printf("Hello, ");
    fputs(name, stdout);  // String output
    
    return 0;
}
```