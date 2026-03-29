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