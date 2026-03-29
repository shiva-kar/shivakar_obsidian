### 71.4 Dependency Injection

```cpp
class Engine {
public:
    virtual void start() = 0;
};
class Car {
    Engine& engine;
public:
    Car(Engine& e): engine(e) {}
    void drive(){ engine.start(); }
};
```

---