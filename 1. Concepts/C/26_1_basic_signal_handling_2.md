### 26.1 Basic Signal Handling
```c
#include <stdio.h>
#include <stdlib.h>
#include <signal.h>
#include <unistd.h>

void signal_handler(int sig) {
    switch (sig) {
        case SIGINT:
            printf("\nReceived SIGINT (Ctrl+C). Cleaning up...\n");
            exit(0);
        case SIGTERM:
            printf("Received SIGTERM. Exiting gracefully...\n");
            exit(0);
        case SIGUSR1:
            printf("Received SIGUSR1. Custom action.\n");
            break;
    }
}

int main() {
    // Register signal handlers
    signal(SIGINT, signal_handler);
    signal(SIGTERM, signal_handler);
    signal(SIGUSR1, signal_handler);
    
    printf("Program started. PID: %d\n", getpid());
    printf("Send SIGUSR1: kill -USR1 %d\n", getpid());
    printf("Press Ctrl+C to exit.\n");
    
    while (1) {
        printf("Working...\n");
        sleep(2);
    }
    
    return 0;
}
```