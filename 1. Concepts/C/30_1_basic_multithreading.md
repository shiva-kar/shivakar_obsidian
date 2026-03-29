### 30.1 Basic Multithreading
```c
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <unistd.h>

#define NUM_THREADS 5

// Thread function
void* printHello(void* threadid) {
    long tid = (long)threadid;
    printf("Hello from thread %ld\n", tid);
    sleep(1);
    printf("Thread %ld finished\n", tid);
    pthread_exit(NULL);
}

int main() {
    pthread_t threads[NUM_THREADS];
    int rc;
    long t;
    
    for (t = 0; t < NUM_THREADS; t++) {
        printf("Creating thread %ld\n", t);
        rc = pthread_create(&threads[t], NULL, printHello, (void*)t);
        
        if (rc) {
            printf("Error creating thread %ld\n", t);
            exit(-1);
        }
    }
    
    // Wait for all threads to complete
    for (t = 0; t < NUM_THREADS; t++) {
        pthread_join(threads[t], NULL);
    }
    
    printf("All threads completed\n");
    pthread_exit(NULL);
}
```