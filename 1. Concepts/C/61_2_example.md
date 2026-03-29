### 61.2 Example

```cpp
#include <atomic>
std::atomic<int> counter = 0;
counter.fetch_add(1, std::memory_order_relaxed);
```

---