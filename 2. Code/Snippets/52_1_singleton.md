### 52.1 Singleton

```cpp
class Singleton {
    Singleton() {}
public:
    static Singleton& instance() {
        static Singleton s;
        return s;
    }
};
```