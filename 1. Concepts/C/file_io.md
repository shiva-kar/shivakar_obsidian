# File I/O

## Core Idea
File I/O persists and retrieves data outside process memory.

## Why it exists
Programs need durable input/output beyond console.

## Mental Model
File handle = resource token; always close it.

## Code Pattern
~~~c
FILE *fp = fopen("data.txt", "r");
if (!fp) return 1;
char line[128];
while (fgets(line, sizeof line, fp)) { }
fclose(fp);
~~~

## Common Mistakes
- Forgetting to close files
- Using wrong mode (text/binary/append)

## Interview Angle
- EOF handling patterns
- Safe parsing from files

## Related
- [[strings]]
- [[functions]]
- [[memory_management]]

## Legacy Notes (archived)
# file io

Merged from legacy micro-notes.

## 13 1 data organization 2

### 13.1 Data Organization
**Storage Types:**
1. **RAM**: Volatile, temporary data storage
2. **ROM**: Non-volatile, firmware storage
3. **HDDs**: Mechanical, magnetic, long-term storage
4. **SSDs**: Fast, non-volatile, flash memory
5. **Cache**: Speedy volatile memory in CPUs
6. **Virtual Memory**: Hard drive used as RAM extension
7. **Flash Memory**: Portable non-volatile storage
8. **Optical Storage**: CDs, DVDs, Blu-ray discs

**C Library Benefits:**
1. **Simplicity**: Simple interface hiding OS complexity
2. **Portability**: Same calls across different OS
3. **Standardization**: Consistent behavior across environments
4. **Ease of Use**: No OS-specific system call knowledge needed
5. **Abstraction**: Manages OS interactions seamlessly

## 13 11 file opening modes

### 13.11 File Opening Modes
- `"r"`: Read (file must exist)
- `"w"`: Write (creates/truncates file)
- `"a"`: Append (creates/appends to file)
- `"r+"`: Read/update (file must exist)
- `"w+"`: Write/update (creates/truncates file)
- `"a+"`: Append/update (creates/appends to file)

## 13 3 text files binary files 2

### 13.3 Text Files & Binary Files
- **Text Files**: Human-readable, character representation
- **Binary Files**: Same as in-memory representation, byte sequence
- **Portability**: Text files more portable across platforms
- **Efficiency**: Binary files more efficient for I/O operations

## 13 4 file pointer 2

### 13.4 File pointer
- Type: `FILE*`
- Standard: `stdin`, `stdout`, `s


## Questions
- When should I use this instead of an alternative?
- What edge case is most likely to break this approach?

