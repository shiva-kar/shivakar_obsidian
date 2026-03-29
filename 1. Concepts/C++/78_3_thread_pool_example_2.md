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