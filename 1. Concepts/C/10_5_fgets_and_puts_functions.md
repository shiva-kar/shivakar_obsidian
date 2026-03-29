### 10.5 fgets and puts functions
**fgets():**
- Safe input from file/stdin into buffer
- Limits length to prevent overflow
- Can include newline if fits in buffer

**puts():**
- Simple output to stdout
- Appends newline automatically
- No formatting options

**gets() (Not Recommended):**
- Unsafe (no size limits)
- Prone to buffer overflow
- Removed from C11 standard