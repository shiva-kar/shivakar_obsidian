### 28.2 Function Pointer Arrays
```c
#include <stdio.h>

void sayHello() {
    printf("Hello!\n");
}

void sayGoodbye() {
    printf("Goodbye!\n");
}

void sayThanks() {
    printf("Thank you!\n");
}

int main() {
    // Array of function pointers
    void (*functions[])() = {sayHello, sayGoodbye, sayThanks};
    
    int choice;
    
    printf("Choose an option (0=Hello, 1=Goodbye, 2=Thanks): ");
    scanf("%d", &choice);
    
    if (choice >= 0 && choice <= 2) {
        functions[choice]();
    } else {
        printf("Invalid choice\n");
    }
    
    return 0;
}
```