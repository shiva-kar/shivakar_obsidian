### 54.2 Move Constructor / Move Assignment

```cpp
class Buffer {
    int* data;
public:
    Buffer(size_t n): data(new int[n]) {}
    ~Buffer(){ delete[] data; }

    Buffer(Buffer&& other) noexcept : data(other.data) {
        other.data = nullptr;
    }

    Buffer& operator=(Buffer&& other) noexcept {
        if(this != &other){
            delete[] data;
            data = other.data;
            other.data = nullptr;
        }
        return *this;
    }
};
```

---