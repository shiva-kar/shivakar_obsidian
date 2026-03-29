### 57.2 Example

```cpp
#include <coroutine>
#include <iostream>

struct Generator {
    struct promise_type {
        int current;
        auto get_return_object() { return Generator{std::coroutine_handle<promise_type>::from_promise(*this)}; }
        std::suspend_always initial_suspend() { return {}; }
        std::suspend_always yield_value(int v){ current = v; return {}; }
        std::suspend_always final_suspend() noexcept { return {}; }
        void return_void() {}
        void unhandled_exception() {}
    };
    std::coroutine_handle<promise_type> handle;
    bool next(){ if(!handle.done()) handle.resume(); return !handle.done(); }
    int value(){ return handle.promise().current; }
};
```

---