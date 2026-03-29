## 26. Concurrency (std::thread & Synchronization)

- `std::thread`, `std::mutex`, `std::lock_guard`, `std::unique_lock`, `std::condition_variable`
    
- Higher-level abstractions: thread pools (3rd party) or `std::async`/`std::future`
    
- Memory model and data races; avoid UB by proper synchronization
    

```cpp
#include <thread>
#include <iostream>

void worker() { std::cout << "worker\n"; }

int main() {
    std::thread t(worker);
    t.join();
}
```