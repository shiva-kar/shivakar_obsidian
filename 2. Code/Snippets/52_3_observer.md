### 52.3 Observer

```cpp
#include <vector>
#include <functional>
class Event {
    std::vector<std::function<void()>> listeners;
public:
    void subscribe(std::function<void()> fn){ listeners.push_back(fn); }
    void notify(){ for(auto& fn: listeners) fn(); }
};
```

---