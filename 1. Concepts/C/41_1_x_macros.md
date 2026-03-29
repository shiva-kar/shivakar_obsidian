### 41.1 X-Macros
```c
#include <stdio.h>

// X-Macro for error codes
#define ERROR_TABLE \
    X(SUCCESS, "No error") \
    X(ERROR_INVALID_INPUT, "Invalid input provided") \
    X(ERROR_OUT_OF_MEMORY, "Memory allocation failed") \
    X(ERROR_FILE_NOT_FOUND, "File not found") \
    X(ERROR_NETWORK, "Network connection failed")

// Generate enum
typedef enum {
    #define X(code, message) code,
    ERROR_TABLE
    #undef X
    ERROR_COUNT
} ErrorCode;

// Generate string array
const char* error_messages[] = {
    #define X(code, message) message,
    ERROR_TABLE
    #undef X
};

const char* get_error_message(ErrorCode code) {
    if (code >= 0 && code < ERROR_COUNT) {
        return error_messages[code];
    }
    return "Unknown error";
}

int main() {
    for (ErrorCode i = SUCCESS; i < ERROR_COUNT; i++) {
        printf("Error %d: %s\n", i, get_error_message(i));
    }
    return 0;
}
```