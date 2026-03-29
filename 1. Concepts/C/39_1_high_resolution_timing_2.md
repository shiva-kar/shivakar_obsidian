### 39.1 High-Resolution Timing
```c
#include <stdio.h>
#include <time.h>

#ifdef _WIN32
    #include <windows.h>
#else
    #include <sys/time.h>
#endif

// Cross-platform high-resolution timer
typedef struct {
#ifdef _WIN32
    LARGE_INTEGER start;
    LARGE_INTEGER frequency;
#else
    struct timespec start;
#endif
} timer_t;

void timer_start(timer_t *timer) {
#ifdef _WIN32
    QueryPerformanceFrequency(&timer->frequency);
    QueryPerformanceCounter(&timer->start);
#else
    clock_gettime(CLOCK_MONOTONIC, &timer->start);
#endif
}

double timer_elapsed(timer_t *timer) {
#ifdef _WIN32
    LARGE_INTEGER end;
    QueryPerformanceCounter(&end);
    return (double)(end.QuadPart - timer->start.QuadPart) / timer->frequency.QuadPart;
#else
    struct timespec end;
    clock_gettime(CLOCK_MONOTONIC, &end);
    return (end.tv_sec - timer->start.tv_sec) + 
           (end.tv_nsec - timer->start.tv_nsec) / 1e9;
#endif
}

void benchmark_function() {
    timer_t timer;
    timer_start(&timer);
    
    // Code to benchmark
    volatile int sum = 0;
    for (int i = 0; i < 1000000; i++) {
        sum += i * i;
    }
    
    double elapsed = timer_elapsed(&timer);
    printf("Function took: %.6f seconds\n", elapsed);
    printf("Sum: %d\n", sum);
}

int main() {
    benchmark_function();
    return 0;
}
```