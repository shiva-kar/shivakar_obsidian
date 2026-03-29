### 54.1 rvalue References

```cpp
void takeString(std::string&& s) { /* uses s */ }
takeString("temp"); // temporary binds to rvalue ref
```