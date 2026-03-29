### 43.2 Atomics

- `<atomic>` types provide lock-free synchronization.
    

```cpp
#include <atomic>
std::atomic<int> counter{0};
counter.fetch_add(1);
```