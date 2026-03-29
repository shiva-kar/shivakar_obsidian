# concurrency

## Core Idea
Consolidated concept from prior micro-notes.

## Legacy Notes (archived)

### 43 1 futures and promises 2

### 43.1 Futures and Promises

```cpp
#include <future>
#include <iostream>

int compute() { return 42; }

int main() {
    std::future<int> result = std::async(compute);
    std::cout << result.get(); // waits for completion
}
```

### 43 3 condition variables 2

### 43.3 Condition Variables

```cpp
#include <condition_variable>
#include <mutex>
#include <thread>
#include <iostream>

std::mutex mtx;
std::condition_variable cv;
bool ready = false;

void worker() {
    std::unique_lock lock(mtx);
    cv.wait(lock, [] { return ready; });
    std::cout << "Worker proceeding\n";
}
```

---

### 43 modern concurrency tools c 11 20 2

## 43. Modern Concurrency Tools (C++11–20)

### 57 coroutines c 20 2

## 57. Coroutines (C++20)

### 78 2 cuda c 2

### 78.2 CUDA C++

```cpp
__global__ void add(int *a, int *b, int *c){
    int i = threadIdx.x;
    c[i] = a[i] + b[i];
}
```

### 78 3 thread pool example 2

### 78.3 Thread Pool Example

```cpp
#include <thread>
#include <queue>
#include <mutex>
#include <condition_variable>
#include <functional>
#include <vector>

class ThreadPool {
    std::vector<std::thread> workers;
    std::queue<std::function<void()>> tasks;
    std::mutex m;
    std::condition_variable cv;
    bool stop = false;
public:
    ThreadPool(size_t n) {
        for(size_t i=0;i<n;i++)
            workers.emplace_back([this]{
                while(true){
                    std::function<void()> task;
                    {
                        std::unique_lock lock(m);
                        cv.wait(lock,[&]{ return stop || !tasks.empty(); });
                        if(stop && tasks.empty()) return;
                        task = std::move(tasks.front());
                        tasks.pop();
                    }
                    task();
                }
            });
    }
    template<class F> void enqueue(F f){
        { std::unique_lock lock(m); tasks.push(std::move(f)); }
        cv.notify_one();
    }
    ~ThreadPool(){
        { std::unique_lock lock(m); stop=true; }
        cv.notify_all();
        for(auto& t: workers) t.join();
    }
};
```

---



## Why it exists
Real engineering problem this concept solves.


## Code Pattern
```c
// minimal reusable example
```


## Common Mistakes
- Misapplying the concept without constraints.
- Ignoring edge cases and failure paths.


## Questions
- When should I use this instead of an alternative?
- What edge case is most likely to break this approach?


## Related
- [[templates]]
- [[stl]]
- [[memory_management]]

