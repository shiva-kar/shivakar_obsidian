# memory management

## Core Idea
Consolidated concept from prior micro-notes.

## Legacy Notes (archived)

### 27 move semantics performance

## 27. Move Semantics & Performance

- Move constructors and move assignment for efficient transfers
    
- `std::move` marks rvalue. Use `std::move` when you want to transfer resources.
    
- Avoid unnecessary copies: use `const T&` or `T&&` appropriately.

### 54 move semantics deep dive

## 54. Move Semantics Deep Dive

### 56 4 capture move c 14 2

### 56.4 Capture Move (C++14)

```cpp
auto ptr = std::make_unique<int>(42);
auto f = [p = std::move(ptr)] { return *p; };
```

---

