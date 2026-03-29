# STL

## Core Idea
Consolidated concept from prior micro-notes.

## Legacy Notes (archived)

### 24 standard template library stl 2

## 24. Standard Template Library (STL)

- Containers: `std::vector`, `std::string`, `std::deque`, `std::list`, `std::set`, `std::map`, `std::unordered_map`
    
- Iterators and iterator categories
    
- Algorithms: `<algorithm>` e.g., `std::sort`, `std::find`, `std::transform`
    
- `std::tuple`, `std::pair`
    
- Example:
    

```cpp
#include <vector>
#include <algorithm>

std::vector<int> v{3,1,4,1,5};
std::sort(v.begin(), v.end());
```

### 40 2 tuple 2

### 40.2 `<tuple>`

- `std::tuple<Ts...>` for grouping heterogeneous values.
    
- Access with `std::get<N>`.
    
- Structured binding (C++17):
    

```cpp
#include <tuple>
#include <iostream>

auto person = std::make_tuple("Alice", 20, 5.7);
auto [name, age, height] = person;
std::cout << name << " " << age << " " << height;
```

### 40 3 chrono time 2

### 40.3 `<chrono>` (Time)

- Types: `std::chrono::duration`, `std::chrono::time_point`
    
- Clock types: `system_clock`, `steady_clock`, `high_resolution_clock`
    
- Usage:
    

```cpp
#include <chrono>
#include <thread>
#include <iostream>

auto start = std::chrono::steady_clock::now();
std::this_thread::sleep_for(std::chrono::seconds(1));
auto end = std::chrono::steady_clock::now();
std::cout << std::chrono::duration_cast<std::chrono::milliseconds>(end - start).count() << "ms";
```

### 40 4 filesystem c 17 2

### 40.4 `<filesystem>` (C++17)

- Filesystem API for paths, directories, file iteration.
    
- Example:
    

```cpp
#include <filesystem>
#include <iostream>
namespace fs = std::filesystem;

int main() {
    for (auto &p : fs::directory_iterator(".")) 
        std::cout << p.path() << '\n';
}
```

---

### 60 parallel stl c 17 2

## 60. Parallel STL (C++17)

### std vector

## 9. Arrays & std::array / std::vector

- C-style arrays still present
    
- Prefer `std::array<T, N>` for fixed-size arrays
    
- Prefer `std::vector<T>` for dynamic arrays (safer, RAII)
    
- Multidimensional arrays vs `std::vector<std::vector<T>>`
    

```cpp
#include <vector>
std::vector<int> v = {1,2,3};
v.push_back(4);
```



## Why it exists
Real engineering problem this concept solves.


## Code Pattern
```c
// minimal reusable example
```


## Common Mistakes
- Misapplying the concept without constraints.
- Ignoring edge cases and failure paths.


## Questions
- When should I use this instead of an alternative?
- What edge case is most likely to break this approach?


## Related
- [[templates]]
- [[stl]]
- [[memory_management]]

