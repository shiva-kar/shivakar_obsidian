### 45.1 Real-time Constraints
```c
#include <stdio.h>
#include <time.h>
#include <sched.h>
#include <sys/mman.h>

void set_real_time_priority() {
    struct sched_param param;
    
    // Lock memory to prevent paging
    mlockall(MCL_CURRENT | MCL_FUTURE);
    
    // Set real-time scheduling policy
    param.sched_priority = sched_get_priority_max(SCHED_FIFO);
    if (sched_setscheduler(0, SCHED_FIFO, &param) == -1) {
        perror("sched_setscheduler");
    }
}

void real_time_delay_ns(long ns) {
    struct timespec req, rem;
    req.tv_sec = 0;
    req.tv_nsec = ns;
    
    // High-precision sleep
    while (nanosleep(&req, &rem) == -1) {
        req = rem;
    }
}

void real_time_task() {
    struct timespec start, end;
    long total_delay = 0;
    const int iterations = 1000;
    
    set_real_time_priority();
    
    for (int i = 0; i < iterations; i++) {
        clock_gettime(CLOCK_MONOTONIC, &start);
        
        // Real-time work
        for (volatile int j = 0; j < 1000; j++) {}
        
        // Precise 1ms delay
        real_time_delay_ns(1000000);  // 1ms
        
        clock_gettime(CLOCK_MONOTONIC, &end);
        
        long delay_ns = (end.tv_sec - start.tv_sec) * 1000000000L + 
                       (end.tv_nsec - start.tv_nsec);
        total_delay += labs(delay_ns - 1000000L);  // Deviation from 1ms
    }
    
    printf("Average timing deviation: %.2f microseconds\n", 
           (double)total_delay / iterations / 1000.0);
}

int main() {
    real_time_task();
    return 0;
}
```