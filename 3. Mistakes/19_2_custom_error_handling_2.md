### 19.2 Custom Error Handling
```c
#include <stdio.h>
#include <stdlib.h>

typedef enum {
    SUCCESS,
    ERROR_NULL_POINTER,
    ERROR_INVALID_INPUT,
    ERROR_OUT_OF_MEMORY
} ErrorCode;

const char* getErrorMessage(ErrorCode code) {
    switch (code) {
        case SUCCESS: return "Success";
        case ERROR_NULL_POINTER: return "Null pointer error";
        case ERROR_INVALID_INPUT: return "Invalid input";
        case ERROR_OUT_OF_MEMORY: return "Out of memory";
        default: return "Unknown error";
    }
}

ErrorCode safeDivide(int a, int b, double *result) {
    if (result == NULL) {
        return ERROR_NULL_POINTER;
    }
    
    if (b == 0) {
        return ERROR_INVALID_INPUT;
    }
    
    *result = (double)a / b;
    return SUCCESS;
}

int main() {
    double result;
    ErrorCode error = safeDivide(10, 0, &result);
    
    if (error != SUCCESS) {
        printf("Error: %s\n", getErrorMessage(error));
        return 1;
    }
    
    printf("Result: %.2f\n", result);
    return 0;
}
```