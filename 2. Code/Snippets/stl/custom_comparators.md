### 55.4 Custom Comparators

```cpp
std::sort(v.begin(), v.end(), [](auto& a, auto& b){ return a.size() < b.size(); });
```

---