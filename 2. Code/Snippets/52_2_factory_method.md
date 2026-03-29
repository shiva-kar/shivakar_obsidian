### 52.2 Factory Method

```cpp
class Shape {
public:
    virtual void draw() = 0;
    static std::unique_ptr<Shape> create(const std::string&);
};
```