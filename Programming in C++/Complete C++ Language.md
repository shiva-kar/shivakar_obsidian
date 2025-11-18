### Installation & Compiler Setup

- What is an IDE
    
- Need for an IDE
    
- Windows installation (MSYS2 + MinGW-w64 or Visual Studio)
    
- macOS installation (Xcode + clang)
    
- Linux installation (g++, clang)
    
- Installing VS Code extensions (C/C++, CMake Tools)
    
- Compiler quick checks: `g++ --version`, `clang++ --version`
    
- Build systems: `g++` CLI, CMake example (basic `CMakeLists.txt`)
    

## 1. First C++ Program

## 1.1 Basic Program Structure

```cpp
#include <iostream>

int main() {
    std::cout << "Hello, World\n";
    return 0;
}
```

- File extension `.cpp`
    
- `main()` signature variations: `int main()`, `int main(int argc, char** argv)`
    

### 1.2 Showing Output / 1.3 Importance of main / 1.4 Comments / 1.5 Compiling & Running

- compile: `g++ -std=c++17 main.cpp -o main`
    
- run: `./main` (Unix) or `main.exe` (Windows)
    
- single-line `//`, multi-line `/* ... */`
    

## 2. Variables, Types & I/O

- Built-in types: `char, short, int, long, long long, float, double, bool, wchar_t`
    
- C++-specific: `std::string`, `std::nullptr_t`
    
- `auto` type deduction
    
- `constexpr`, `const`
    
- I/O: `std::cin`, `std::cout`, `std::cerr`, `std::getline`
    

```cpp
#include <iostream>
#include <string>

int main() {
    std::string name;
    std::cout << "Enter name: ";
    std::getline(std::cin, name);
    std::cout << "Hello, " << name << '\n';
}
```

## 3. Expressions & Operators

- Arithmetic, relational, logical, bitwise (same as C)
    
- Additional: scope resolution `::`, `.*` and `->*` (pointer-to-member).
    
- Overloadable operators (see Operator Overloading section).
    

## 4. Decision Control Structures

- `if`, `else`, `else if`, ternary `?:`, `switch` (works with integral/enum types)
    
- `goto` discouraged
    
- Use `std::optional` pattern instead of sentinel values for some cases (C++17)
    

## 5. Loops

- `for`, `while`, `do-while`
    
- Range-based for (C++11): `for (auto &x : container) { }`
    

## 6. Functions and Recursion

- Function declarations, default parameters, inline functions
    
- `constexpr` functions (evaluated at compile-time when possible)
    
- Function overloading
    
- `noexcept` specification
    
- Passing by value, by pointer, by reference, `const &` for efficiency
    

```cpp
int sum(int a, int b = 0) { return a + b; }
```

## 7. Pointers & References

- Raw pointers: declaration, `new`/`delete` (prefer smart pointers)
    
- Pointer to pointer
    
- References: `int &r = x;` (cannot be null, must be initialized)
    
- `nullptr` vs `NULL`
    
- `std::addressof`, `std::exchange` basics
    

```cpp
int x = 10;
int *p = &x;
int &r = x;
```

## 8. Storage Duration & Type Modifiers

- `static`, `extern`, `thread_local`
    
- `signed`/`unsigned`, `short`/`long`
    
- `mutable` (for `const` object member mutation)
    
- Storage classes and linkage differences in C++
    

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

## 10. Strings

- `std::string` is the primary string type
    
- C-style strings (`char*`) exist but are error-prone
    
- Common methods: `.size()`, `.substr()`, `.find()`, `.c_str()`
    
- `std::string_view` (non-owning view, C++17)
    

## 11. Structs and Classes (OOP)

- `struct` vs `class` (default public vs private)
    
- Access specifiers: `public`, `protected`, `private`
    
- Member functions, data members
    
- Constructors, destructors
    
- `this` pointer
    
- `friend` functions/classes
    
- Example:
    

```cpp
#include <string>
#include <iostream>

class Person {
public:
    Person(std::string n, int a): name(std::move(n)), age(a) {}
    void greet() const { std::cout << "Hi, I'm " << name << '\n'; }
private:
    std::string name;
    int age;
};
```

## 12. Dynamic Memory & RAII

- Prefer RAII: resources owned by objects and freed in destructors
    
- Raw `new`/`delete` are legal but discouraged
    
- Use smart pointers (`std::unique_ptr`, `std::shared_ptr`, `std::weak_ptr`)
    
- `std::make_unique`, `std::make_shared`
    

```cpp
#include <memory>

auto p = std::make_unique<int>(42); // unique_ptr<int>
```

## 13. Files I/O

- `<fstream>`: `std::ifstream`, `std::ofstream`, `std::fstream`
    
- Binary vs text modes
    
- Use RAII to manage files (destructor closes file)
    

## 14. Preprocessor & Macros

- `#include`, `#define`, conditional compilation (`#ifdef`) still present
    
- Prefer `constexpr`, `inline` functions and `enum class` over macros
    
- `static_assert` for compile-time checks
    

## 15. Command Line Arguments

- `int main(int argc, char *argv[])`
    
- Prefer `std::string_view`/`std::string` for argument parsing
    
- Use libraries for complex parsing (e.g., `getopt`, `args`, `Boost.Program_options`)
    

## 16. Bitwise Operations

- Same operators as C
    
- Use `std::bitset` for safer bit manipulation
    
- Examples: masking, shifting, flags using `enum class` with bit operations
    

## 17. Unions & std::variant

- Unions exist but have restrictions
    
- Prefer `std::variant` (C++17) for type-safe discriminated unions
    

## 18. Enumerations

- `enum class` (scoped enums) prefered over plain `enum`
    
- Typed enums: `enum class Color : uint8_t { Red, Green, Blue };`
    

## 19. Error Handling

- Exceptions: `try`, `catch`, `throw`
    
- Prefer typed exceptions; avoid using exceptions for control-flow in performance-critical code
    
- `std::error_code` / `std::expected` (proposal/3rd-party libs) for alternate patterns
    
- `noexcept` for functions that must not throw
    

```cpp
try {
    throw std::runtime_error("error");
} catch (const std::exception &e) {
    std::cerr << e.what() << '\n';
}
```

## 20. Templates (Functions & Classes)

- Function templates
    
- Class templates
    
- Template specialization and partial specialization
    
- Variadic templates (C++11)
    
- `typename` vs `class` keyword usage in templates
    
- Example:
    

```cpp
template<typename T>
T add(T a, T b) { return a + b; }

template<typename T>
class Box {
public:
    Box(T v): val(v) {}
    T get() const { return val; }
private:
    T val;
};
```

## 21. Inline, constexpr, consteval

- `inline` functions and variables (C++17 inline variables)
    
- `constexpr` functions and variables (compile-time evaluation)
    
- `consteval` (C++20) forces compile-time evaluation
    

## 22. Modern C++ Features (C++11, C++14, C++17, C++20)

- Move semantics: rvalue references `T&&`, `std::move`, `std::forward`
    
- Rule of Five: destructor, copy ctor, copy assignment, move ctor, move assignment
    
- `= default`, `= delete`
    
- Lambdas: `[capture](args){ body }` (C++11)
    
- `auto` for type deduction
    
- Structured bindings (C++17)
    
- `std::optional`, `std::variant`, `std::any` (C++17)
    
- Concepts (C++20) — optional advanced topic
    

Example lambda:

```cpp
auto sum = [](int a, int b){ return a + b; };
```

## 23. Smart Pointers (detailed)

- `std::unique_ptr<T>`: sole ownership, lightweight
    
- `std::shared_ptr<T>`: reference-counted
    
- `std::weak_ptr<T>`: observe `shared_ptr` without ownership
    
- Use `unique_ptr` when ownership is unique. Use `shared_ptr` when shared ownership required.
    

```cpp
#include <memory>
struct Node { int val; std::unique_ptr<Node> next; };
```

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

## 25. Function Pointers, std::function & Callables

- Function pointers exist
    
- `std::function` and `std::bind`, lambdas for higher-level callables
    

```cpp
#include <functional>
std::function<int(int,int)> op = [](int a,int b){ return a+b; };
```

## 26. Concurrency (std::thread & Synchronization)

- `std::thread`, `std::mutex`, `std::lock_guard`, `std::unique_lock`, `std::condition_variable`
    
- Higher-level abstractions: thread pools (3rd party) or `std::async`/`std::future`
    
- Memory model and data races; avoid UB by proper synchronization
    

```cpp
#include <thread>
#include <iostream>

void worker() { std::cout << "worker\n"; }

int main() {
    std::thread t(worker);
    t.join();
}
```

## 27. Move Semantics & Performance

- Move constructors and move assignment for efficient transfers
    
- `std::move` marks rvalue. Use `std::move` when you want to transfer resources.
    
- Avoid unnecessary copies: use `const T&` or `T&&` appropriately.
    

## 28. Templates Advanced: SFINAE, Traits, and Concepts

- SFINAE (Substitution Failure Is Not An Error)
    
- `std::enable_if`, `std::is_same`, `std::decay`, type traits
    
- C++20 Concepts to write clearer constraints
    

## 29. Variadic Templates & Parameter Packs

- Implement `printf`-like functionality with type safety using variadic templates
    
- Example skeleton:
    

```cpp
template<typename... Args>
void log(Args&&... args) {
    (std::cout << ... << args) << '\n'; // fold expression (C++17)
}
```

## 30. Namespaces & Linkage

- `namespace` for scope and preventing name collisions
    
- `inline namespace` and `anonymous namespace`
    
- `extern "C"` for C interop
    

## 31. Operator Overloading

- Overload operators as member or non-member functions
    
- Common overloads: `operator+`, `operator=`, `operator<<` (stream insertion)
    
- Keep semantics intuitive
    

```cpp
#include <iostream>

struct Vec {
    int x,y;
    Vec(int a,int b):x(a),y(b){}
    Vec operator+(const Vec& o) const { return Vec(x+o.x,y+o.y); }
};

std::ostream& operator<<(std::ostream& os, const Vec& v) {
    return os << '(' << v.x << ',' << v.y << ')';
}
```

## 32. Polymorphism & Inheritance

- Virtual functions, `virtual` destructor
    
- Pure virtual functions (`= 0`) and abstract base classes
    
- Runtime polymorphism via pointers/references to base
    
- Multiple inheritance caveats and virtual base classes
    

## 33. Memory Management Advanced & Undefined Behavior

- Undefined behavior sources: use-after-free, double-delete, data races
    
- Tools: sanitizers (`-fsanitize=address,undefined`), valgrind
    
- Best practices: prefer RAII and smart pointers
    

## 34. Build Systems & Tooling

- `g++` flags (`-std=c++17`, `-O2`, `-g`, `-Wall`, `-Wextra`)
    
- CMake example:
    

```cmake
cmake_minimum_required(VERSION 3.10)
project(MyApp CXX)
set(CMAKE_CXX_STANDARD 17)
add_executable(myapp main.cpp)
```

- Use clang-tidy, clang-format for style and static analysis
    

## 35. Advanced Topics (brief)

- Template metaprogramming
    
- Expression templates
    
- Inline assembly (rare)
    
- Interfacing with C and system APIs
    
- ABI stability and ODR (One Definition Rule)
    
- Coroutines (C++20)
    
- Modules (C++20)
    

## 36. Networking & Sockets (brief)

- C++ has no standard socket library; use Boost.Asio or OS APIs.
    
- Example: use `boost::asio` for cross-platform networking.
    

## 37. Security & Cryptography (brief)

- Use vetted libraries for crypto (OpenSSL, libsodium). Avoid homebrewed crypto.
    
- Memory safety and bounds checks.
    

## 38. Cross-platform Development

- Platform detection macros
    
- Conditional compilation with `#if defined(_WIN32)` etc.
    
- Use CMake for portability.
    

## 39. Examples (selected, complete)

### Hello World

```cpp
#include <iostream>
int main(){ std::cout << "Hello, World\n"; }
```

### Class + RAII example

```cpp
#include <iostream>
#include <fstream>
#include <string>

class Logger {
    std::ofstream out;
public:
    Logger(const std::string &file): out(file) {}
    void log(const std::string &s) { out << s << '\n'; }
    // destructor closes ofstream automatically
};
```

### Template function

```cpp
#include <iostream>

template<typename T>
T add(T a, T b) { return a + b; }

int main() {
    std::cout << add<int>(2,3) << '\n';
}
```

### unique_ptr example

```cpp
#include <memory>
#include <iostream>

struct Node { int v; std::unique_ptr<Node> next; };

int main() {
    auto head = std::make_unique<Node>();
    head->v = 1;
    head->next = std::make_unique<Node>();
    head->next->v = 2;
}
```

### Move semantics example

```cpp
#include <string>
#include <utility>

struct S {
    std::string data;
    S(std::string d): data(std::move(d)) {}
    S(S&&) = default;
    S& operator=(S&&) = default;
};
```

### Lambda + STL example

```cpp
#include <vector>
#include <algorithm>
#include <iostream>

int main() {
    std::vector<int> v{3,1,4,1,5};
    std::sort(v.begin(), v.end(), [](int a, int b){ return a < b; });
    for (int x : v) std::cout << x << ' ';
}
```

## 40. Standard Library Utilities

### 40.1 `<utility>`

- `std::pair`, `std::move`, `std::forward`, `std::swap`
    
- `std::exchange`: assigns a new value and returns the old one.
    

```cpp
#include <utility>
int x = 10;
int y = std::exchange(x, 20); // y=10, x=20
```

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

## 41. Memory Management Deep Dive

### 41.1 Object Lifetime

- Automatic: stack allocation, destroyed when scope ends.
    
- Dynamic: created via `new`/`delete`, managed manually.
    
- RAII and smart pointers ensure deterministic cleanup.
    

### 41.2 Allocation Functions

- Overriding `operator new` and `operator delete` possible for custom allocators.
    
- Use `std::allocator` or `std::pmr::polymorphic_allocator` for advanced control.
    

### 41.3 Smart Pointer Interactions

- Never mix raw and smart pointers for the same object.
    
- Use `weak_ptr` to break circular ownership in graphs.
    

---

## 42. Advanced Templates

### 42.1 Template Specialization

```cpp
template<typename T>
void printType() { std::cout << "Generic type\n"; }

template<>
void printType<int>() { std::cout << "int type\n"; }
```

### 42.2 Partial Specialization

```cpp
template<typename T, typename U>
struct Pair { };

template<typename T>
struct Pair<T, T> { }; // specialized when both same type
```

### 42.3 Variadic Templates & Fold Expressions

```cpp
template<typename... Args>
void printAll(Args&&... args) {
    (std::cout << ... << args) << '\n';
}
```

---

## 43. Modern Concurrency Tools (C++11–20)

### 43.1 Futures and Promises

```cpp
#include <future>
#include <iostream>

int compute() { return 42; }

int main() {
    std::future<int> result = std::async(compute);
    std::cout << result.get(); // waits for completion
}
```

### 43.2 Atomics

- `<atomic>` types provide lock-free synchronization.
    

```cpp
#include <atomic>
std::atomic<int> counter{0};
counter.fetch_add(1);
```

### 43.3 Condition Variables

```cpp
#include <condition_variable>
#include <mutex>
#include <thread>
#include <iostream>

std::mutex mtx;
std::condition_variable cv;
bool ready = false;

void worker() {
    std::unique_lock lock(mtx);
    cv.wait(lock, [] { return ready; });
    std::cout << "Worker proceeding\n";
}
```

---

## 44. Compile-time Programming

### 44.1 `constexpr` and `consteval`

```cpp
constexpr int sqr(int n) { return n * n; }
consteval int cube(int n) { return n * n * n; } // must run at compile time
```

### 44.2 Type Traits

- `<type_traits>` defines meta-functions for compile-time reflection.
    

```cpp
#include <type_traits>
static_assert(std::is_integral<int>::value);
```

---

## 45. Error and Resource Safety Principles

- Use RAII and smart pointers.
    
- Prefer `std::vector` over dynamic arrays.
    
- Use exceptions for recoverable runtime errors.
    
- Use `assert()` for programmer errors and `static_assert()` for compile-time guarantees.
    
- Always ensure strong exception safety (operations either succeed fully or leave state unchanged).
    

---

## 46. Input/Output Advanced Topics

### 46.1 Manipulators

```cpp
#include <iomanip>
std::cout << std::setw(10) << std::setfill('0') << 42;
```

### 46.2 Binary I/O

```cpp
#include <fstream>
int x = 100;
std::ofstream out("data.bin", std::ios::binary);
out.write(reinterpret_cast<char*>(&x), sizeof(x));
```

---

## 47. Debugging & Diagnostics

- Compile with `-g -O0 -Wall -Wextra`.
    
- Use sanitizers:
    
    - AddressSanitizer (`-fsanitize=address`)
        
    - UndefinedBehaviorSanitizer (`-fsanitize=undefined`)
        
- Logging frameworks: spdlog, glog
    
- Assertions for runtime checks.
    

---

## 48. Coding Best Practices

1. Avoid raw pointers for ownership.
    
2. Prefer `std::vector` or `std::array` over raw arrays.
    
3. Pass large objects by reference.
    
4. Minimize `using namespace std;`
    
5. Use `enum class` instead of `#define` constants.
    
6. Prefer modern features (`auto`, range-for, RAII).
    
7. Always initialize variables.
    
8. Use consistent naming conventions.
    
9. Use tools: `clang-tidy`, `cppcheck`, `clang-format`.
    

---

## 49. Complete Sample Program (Combines Multiple Concepts)

```cpp
#include <iostream>
#include <vector>
#include <memory>
#include <algorithm>

class Shape {
public:
    virtual double area() const = 0;
    virtual ~Shape() = default;
};

class Circle : public Shape {
    double r;
public:
    explicit Circle(double radius): r(radius) {}
    double area() const override { return 3.14159 * r * r; }
};

class Rectangle : public Shape {
    double w, h;
public:
    Rectangle(double width, double height): w(width), h(height) {}
    double area() const override { return w * h; }
};

int main() {
    std::vector<std::unique_ptr<Shape>> shapes;
    shapes.push_back(std::make_unique<Circle>(5.0));
    shapes.push_back(std::make_unique<Rectangle>(3.0, 4.0));

    double total = 0;
    for (auto& s : shapes) total += s->area();
    std::cout << "Total area: " << total << '\n';
}
```

**Demonstrates:** classes, inheritance, virtual functions, smart pointers, STL container, loop, polymorphism, RAII.

## 50. Exception Handling Advanced Concepts

### 50.1 Exception Hierarchy

- All standard exceptions derive from `std::exception`.
    
- Common types:
    
    - `std::runtime_error`
        
    - `std::logic_error`
        
    - `std::invalid_argument`
        
    - `std::out_of_range`
        
    - `std::bad_alloc`
        

### 50.2 Custom Exception Class

```cpp
#include <stdexcept>
class FileError : public std::runtime_error {
public:
    explicit FileError(const std::string &msg) : std::runtime_error(msg) {}
};
```

### 50.3 Best Practices

- Throw by value, catch by reference.
    
- Avoid exceptions in destructors.
    
- Always provide `noexcept` where exceptions must not propagate.
    

---

## 51. Namespaces and Modularization

### 51.1 Namespaces

- Group related declarations and avoid symbol collisions.
    

```cpp
namespace math {
    double square(double x) { return x * x; }
}
```

Access with `math::square(5)`.

### 51.2 Nested Namespaces

```cpp
namespace graphics::shapes {
    class Circle {};
}
```

### 51.3 Inline and Anonymous Namespaces

- `inline namespace` allows versioning.
    
- `namespace { }` gives internal linkage (local to translation unit).
    

### 51.4 Modules (C++20)

- Replace headers and preprocessor with compiled interfaces.
    

```cpp
export module math;
export int add(int a, int b) { return a + b; }
```

---

## 52. Design Patterns (C++ Implementation)

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

### 52.2 Factory Method

```cpp
class Shape {
public:
    virtual void draw() = 0;
    static std::unique_ptr<Shape> create(const std::string&);
};
```

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

## 53. Generic Programming & Type Deduction

### 53.1 Template Argument Deduction

- Compiler deduces template parameters automatically:
    

```cpp
template<typename T>
void f(T x) { }
f(42); // deduces T = int
```

### 53.2 Trailing Return Type

```cpp
template<typename T, typename U>
auto add(T a, U b) -> decltype(a + b) { return a + b; }
```

### 53.3 `decltype` and `decltype(auto)`

Used for type introspection.

```cpp
int x = 5;
decltype(x) y = 10; // y is int
```

---

## 54. Move Semantics Deep Dive

### 54.1 rvalue References

```cpp
void takeString(std::string&& s) { /* uses s */ }
takeString("temp"); // temporary binds to rvalue ref
```

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

## 55. Standard Algorithms in Depth

### 55.1 Non-modifying

`std::find`, `std::count`, `std::all_of`, `std::any_of`, `std::none_of`

### 55.2 Modifying

`std::copy`, `std::transform`, `std::remove_if`, `std::replace`

### 55.3 Sorting and Searching

`std::sort`, `std::binary_search`, `std::lower_bound`, `std::unique`

### 55.4 Custom Comparators

```cpp
std::sort(v.begin(), v.end(), [](auto& a, auto& b){ return a.size() < b.size(); });
```

---

## 56. Lambda Expressions Advanced

### 56.1 Capture Modes

- `[=]` captures by value
    
- `[&]` captures by reference
    
- `[this]` captures current object
    

### 56.2 Mutable Lambdas

```cpp
int x = 10;
auto f = [x]() mutable { x++; return x; };
```

### 56.3 Generic Lambdas

```cpp
auto add = [](auto a, auto b){ return a + b; };
```

### 56.4 Capture Move (C++14)

```cpp
auto ptr = std::make_unique<int>(42);
auto f = [p = std::move(ptr)] { return *p; };
```

---

## 57. Coroutines (C++20)

### 57.1 Basics

Enable cooperative multitasking using `co_await`, `co_yield`, `co_return`.

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

## 58. File and Stream Customization

### 58.1 Overloading Stream Operators

```cpp
class Point {
public:
    int x, y;
};
std::ostream& operator<<(std::ostream& os, const Point& p){
    return os << "(" << p.x << "," << p.y << ")";
}
```

### 58.2 Stream States

- `good()`, `fail()`, `eof()`, `bad()`
    
- Use `exceptions()` to enable automatic exception throwing.
    

---

## 59. STL Containers Deep Dive

|Container|Type|Key Features|
|---|---|---|
|`vector`|Sequential|Dynamic contiguous array|
|`list`|Sequential|Doubly linked|
|`deque`|Sequential|Double-ended|
|`set`|Associative|Ordered, unique|
|`map`|Associative|Key-value ordered|
|`unordered_map`|Hash-based|Fast lookup|
|`priority_queue`|Adapter|Max-heap by default|

### Example:

```cpp
#include <unordered_map>
std::unordered_map<std::string, int> freq;
freq["apple"]++;
```

---

## 60. Parallel STL (C++17)

### 60.1 Parallel Execution Policies

`std::execution::seq`, `std::execution::par`, `std::execution::par_unseq`

```cpp
#include <execution>
#include <algorithm>
std::sort(std::execution::par, v.begin(), v.end());
```

---

## 61. C++ Memory Model and Atomics

### 61.1 Memory Order

- `memory_order_relaxed`
    
- `memory_order_acquire`
    
- `memory_order_release`
    
- `memory_order_seq_cst`
    

### 61.2 Example

```cpp
#include <atomic>
std::atomic<int> counter = 0;
counter.fetch_add(1, std::memory_order_relaxed);
```

---

## 62. Localization and Internationalization

### 62.1 Locales

```cpp
#include <locale>
std::locale loc("en_US.UTF-8");
std::cout.imbue(loc);
```

### 62.2 Wide Strings

- Use `std::wstring`, `std::wcout`, and `L"wide literal"` for Unicode text.
    

---

## 63. Interfacing C and C++

### 63.1 extern "C"

Used to link C functions without name mangling:

```cpp
extern "C" void c_func();
```

### 63.2 Mixing C and C++ Code

- C++ code can call C libraries by wrapping headers in:
    

```cpp
#ifdef __cplusplus
extern "C" {
#endif
// C declarations
#ifdef __cplusplus
}
#endif
```

---

## 64. Linking, Compilation, and Build Pipelines

### 64.1 Compilation Stages

1. Preprocessing
    
2. Compilation
    
3. Assembly
    
4. Linking
    

### 64.2 Static vs Shared Libraries

- Static: `.a` or `.lib`
    
- Shared: `.so` or `.dll`
    

### 64.3 Example Commands

```bash
g++ -c util.cpp
ar rcs libutil.a util.o
g++ main.cpp -L. -lutil -o app
```

---

## 65. Testing in C++

### 65.1 Unit Testing Frameworks

- **GoogleTest (gtest)**
    
- **Catch2**
    
- **Doctest**
    

### 65.2 Example (Catch2)

```cpp
#define CATCH_CONFIG_MAIN
#include "catch.hpp"
int add(int a, int b){ return a+b; }
TEST_CASE("Addition", "[math]") {
    REQUIRE(add(2,3) == 5);
}
```

---

## 66. Profiling and Optimization

### 66.1 Tools

- Linux: `gprof`, `perf`
    
- Windows: Visual Studio Profiler
    
- Instruments: Valgrind, cachegrind
    

### 66.2 Optimization Flags

`-O2`, `-O3`, `-flto`, `-march=native`

### 66.3 Best Practices

- Avoid premature optimization.
    
- Measure before and after.
    
- Prefer algorithmic improvement over micro-optimization.
    

---

## 67. Reflection and Introspection (C++20+ proposals)

### 67.1 Runtime Type Information (RTTI)

- `typeid(obj)` returns type info.
    
- `dynamic_cast` for downcasting polymorphic types.
    

### 67.2 Static Reflection (planned for future)

- Compile-time introspection of class structure.
   **Static reflection** is a programming feature that allows a program to inspect its own code and structure at **compile time** rather than runtime. Unlike dynamic reflection which occurs while the program is running, static reflection uses information collected during the compilation process to generate optimized code or perform compile-time checks. This leads to higher performance and zero-overhead abstractions, and is especially useful in statically-typed languages like C++. 

Key characteristics

- **Compile-time process:** All reflection and code generation happens during the compilation phase, before the program is executed.
- **Compiler-based:** The compiler is responsible for collecting type and code information and using it to transform the code.
- **High performance:** Because it runs at compile time, it can lead to highly optimized code without the performance overhead associated with runtime reflection.
- **Compile-time safety:** The use of compile-time checks can catch errors early in the development process.
- **Limited by compiler knowledge:** It can only be used on code that the compiler knows about, as it relies on information available during compilation. 

Example scenarios

- **Code generation:** Automatically generating code for tasks like serialization, data validation, or creating boilerplate code based on a class's structure.
- **Compile-time validation:** Performing type-checking or other checks at compile time to ensure the generated code is correct and meets specific requirements.
- **Metaprogramming:** Creating complex compile-time algorithms or abstractions, such as creating a  a make_integer_sequence for a specific type.

## 68. Networking in C++

### 68.1 Standard and Third-Party Libraries

C++ has no official networking API until C++23. Common options:

- **Boost.Asio** (cross-platform, low-level)
    
- **cpp-httplib** (header-only HTTP)
    
- **cpr** (modern HTTP client wrapper)
    
- **Qt Network** (event-driven networking)
    

### 68.2 TCP Server Example (Boost.Asio)

```cpp
#include <boost/asio.hpp>
using boost::asio::ip::tcp;

int main() {
    boost::asio::io_context io;
    tcp::acceptor acceptor(io, tcp::endpoint(tcp::v4(), 8080));
    tcp::socket socket(io);
    acceptor.accept(socket);
    boost::asio::write(socket, boost::asio::buffer("Hello, Client\n"));
}
```

### 68.3 HTTP Client Example (cpr)

```cpp
#include <cpr/cpr.h>
#include <iostream>

int main() {
    auto r = cpr::Get(cpr::Url{"https://example.com"});
    std::cout << r.status_code << "\n" << r.text;
}
```

---

## 69. GUI Development in C++

### 69.1 Common Frameworks

- **Qt** – cross-platform, mature
    
- **wxWidgets** – native look & feel
    
- **ImGui** – lightweight, immediate mode GUI
    
- **SFML** / **SDL** – multimedia/game development
    

### 69.2 Qt Example

```cpp
#include <QApplication>
#include <QLabel>

int main(int argc, char *argv[]) {
    QApplication app(argc, argv);
    QLabel label("Hello, Qt!");
    label.show();
    return app.exec();
}
```

---

## 70. Embedded Systems with C++

### 70.1 Characteristics

- No dynamic memory
    
- Limited standard library
    
- Hardware-specific I/O
    
- Deterministic timing required
    

### 70.2 Example: Bare-metal LED toggle

```cpp
#include <stdint.h>
#define LED_PORT *((volatile uint32_t*)0x40021018)

int main() {
    while (1) {
        LED_PORT ^= 1;  // toggle LED
        for (volatile int i = 0; i < 100000; ++i);
    }
}
```

### 70.3 Best Practices

- Avoid exceptions and RTTI.
    
- Use fixed-size containers (`std::array`).
    
- Use `constexpr` and templates for compile-time operations.
    

---

## 71. C++ Software Architecture Principles

### 71.1 RAII (Resource Acquisition Is Initialization)

- Acquire resources in constructors, release in destructors.
    

### 71.2 SOLID Principles

1. **Single Responsibility**
    
2. **Open/Closed**
    
3. **Liskov Substitution**
    
4. **Interface Segregation**
    
5. **Dependency Inversion**
    

### 71.3 Layered Design Example

- **Domain Layer:** classes, logic
    
- **Data Layer:** persistence, serialization
    
- **Presentation Layer:** CLI/GUI
    

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

## 72. Serialization and Persistence

### 72.1 Text-Based (JSON, XML)

- Libraries: nlohmann/json, rapidjson, pugixml
    

```cpp
#include <nlohmann/json.hpp>
#include <iostream>
using json = nlohmann::json;

int main() {
    json j = { {"name", "Alice"}, {"age", 25} };
    std::cout << j.dump(4);
}
```

### 72.2 Binary Serialization

- Use `<fstream>` or libraries like cereal, protobuf.
    

```cpp
#include <cereal/archives/binary.hpp>
#include <fstream>

struct Data { int x; template<class Ar> void serialize(Ar& ar){ ar(x); } };
```

---

## 73. Logging Systems

### 73.1 Simple Logging

```cpp
#include <iostream>
#define LOG(x) std::cout << __FILE__ << ":" << __LINE__ << " " << x << "\n"
```

### 73.2 Using spdlog

```cpp
#include <spdlog/spdlog.h>
int main() {
    spdlog::info("Hello from spdlog!");
}
```

### 73.3 Log Levels

Trace → Debug → Info → Warn → Error → Critical

---

## 74. Cross-Platform Development

### 74.1 Conditional Compilation

```cpp
#ifdef _WIN32
    system("cls");
#else
    system("clear");
#endif
```

### 74.2 CMake Configuration

```cmake
if(WIN32)
    add_definitions(-DWINDOWS_BUILD)
elseif(UNIX)
    add_definitions(-DLINUX_BUILD)
endif()
```

### 74.3 Portability Guidelines

- Avoid platform APIs directly.
    
- Use `std::filesystem`, `std::thread`, `std::chrono` instead of OS calls.
    
- Test on multiple compilers.
    

---

## 75. Game Development Basics

### 75.1 Common Frameworks

- **SFML**
    
- **SDL2**
    
- **Raylib**
    
- **Unreal Engine (C++)**
    

### 75.2 Simple SFML Example

```cpp
#include <SFML/Graphics.hpp>

int main() {
    sf::RenderWindow window(sf::VideoMode(800, 600), "Game");
    sf::CircleShape circle(50);
    while (window.isOpen()) {
        sf::Event event;
        while (window.pollEvent(event))
            if (event.type == sf::Event::Closed) window.close();
        window.clear();
        window.draw(circle);
        window.display();
    }
}
```

---

## 76. Security and Safe Coding

### 76.1 Avoid Common Issues

- Buffer overflows
    
- Dangling pointers
    
- Race conditions
    
- Integer overflows
    

### 76.2 Secure Coding Guidelines

- Use bounds-checked containers.
    
- Validate all input.
    
- Prefer RAII for resource control.
    
- Avoid `strcpy`, `sprintf` — use `std::snprintf`, `std::string`.
    

### 76.3 Cryptographic Libraries

Use:

- OpenSSL
    
- libsodium
    
- Botan
    

Never implement your own cryptography.

---

## 77. Interfacing with Other Languages

### 77.1 C Interfacing

Already covered via `extern "C"`.

### 77.2 Python Integration

- **pybind11** and **Boost.Python**
    

```cpp
#include <pybind11/pybind11.h>
int add(int a, int b){ return a+b; }
PYBIND11_MODULE(example, m){ m.def("add", &add); }
```

### 77.3 Rust or Java Interop

- Through FFI (Foreign Function Interface).
    
- Use `.so` or `.dll` as bridges.
    

---

## 78. Parallel and GPU Programming

### 78.1 OpenMP

```cpp
#include <omp.h>
#pragma omp parallel for
for(int i = 0; i < 1000; ++i){ /* work */ }
```

### 78.2 CUDA C++

```cpp
__global__ void add(int *a, int *b, int *c){
    int i = threadIdx.x;
    c[i] = a[i] + b[i];
}
```

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

## 79. Advanced Compilation and Linking Techniques

### 79.1 Link-Time Optimization

`-flto` merges translation units for better performance.

### 79.2 Precompiled Headers

```bash
g++ -std=c++20 -x c++-header common.hpp -o common.hpp.gch
```

### 79.3 Static and Dynamic Analysis Tools

- **clang-tidy**
    
- **cppcheck**
    
- **AddressSanitizer**, **UBSan**
    

---

## 80. Final Notes and Modern C++ Philosophy

1. Write **safe**, **clean**, and **deterministic** code.
    
2. Use **value semantics** over raw pointers.
    
3. RAII and smart pointers replace manual memory control.
    
4. Prefer **STL** and **standard libraries** over custom code.
    
5. Follow **C++ Core Guidelines (Bjarne Stroustrup & Herb Sutter)**.