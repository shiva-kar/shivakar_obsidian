### 12.5 Using realloc
- Resizes previously allocated memory
- Preserves existing data when possible
- If passed `NULL`, behaves like `malloc`
- If size is 0, behaves like `free`
- Returns new pointer (may differ from original)
- Check return value before use