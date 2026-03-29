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
- Standard: `stdin`, `stdout`, `stderr`
- Associated with file via `fopen`
- Used for reading/writing operations
- Tracks current file position
- Should be passed to `fclose`

## 13 5 open a file 2

### 13.5 Open a File
- `fopen()` function returns `FILE*` pointer
- Modes: `r` (read), `w` (write), `a` (append), etc.
- Returns `NULL` on failure
- Always check for successful opening
- Can use relative or absolute paths

## 13 6 close a file

### 13.6 Close a File
- `fclose()` closes open file
- Releases system resources
- Flushes any remaining buffer data
- Good practice to set pointer to `NULL` after closing
- Check return value for success (0) or error (EOF)

## 13 7 reading data from file 2

### 13.7 Reading data from File
- Functions: `fgetc`, `fgets`, `fread`, `fscanf`
- Modes: `"r"` (read), `"r+"` (read/update)
- Ensure proper buffer sizing
- Choose functions based on file type (text/binary)

## 13 8 end of file eof

### 13.8 End of File (EOF)
- Constant indicating file end or error
- Typically `-1` in C libraries
- Used by functions like `fgetc()` for end detection
- Can signal operation failures
- Common in file reading loops

## 13 9 writing data to a file 2

### 13.9 Writing data to a File
- Functions: `fputc`, `fputs`, `fwrite`, `fprintf`
- Modes: `"w"` (write), `"a"` (append), `"w+"`, `"a+"` (update)
- `fflush()` forces buffer write to file
- Choose function/mode based on file type

## 27 1 random file access

### 27.1 Random File Access
```c
#include <stdio.h>
#include <stdlib.h>

typedef struct {
    int id;
    char name[50];
    double salary;
} Employee;

void writeEmployees() {
    FILE *file = fopen("employees.dat", "wb");
    if (!file) {
        perror("Failed to open file");
        return;
    }
    
    Employee employees[] = {
        {1, "John Doe", 50000.0},
        {2, "Jane Smith", 60000.0},
        {3, "Bob Johnson", 55000.0}
    };
    
    fwrite(employees, sizeof(Employee), 3, file);
    fclose(file);
}

void readEmployee(int recordNum) {
    FILE *file = fopen("employees.dat", "rb");
    if (!file) {
        perror("Failed to open file");
        return;
    }
    
    Employee emp;
    
    // Seek to specific record
    fseek(file, (recordNum - 1) * sizeof(Employee), SEEK_SET);
    
    if (fread(&emp, sizeof(Employee), 1, file) == 1) {
        printf("Record %d: ID=%d, Name=%s, Salary=%.2f\n", 
               recordNum, emp.id, emp.name, emp.salary);
    } else {
        printf("Record %d not found\n", recordNum);
    }
    
    fclose(file);
}

int main() {
    writeEmployees();
    
    printf("Reading individual records:\n");
    readEmployee(1);
    readEmployee(2);
    readEmployee(3);
    
    return 0;
}
```

## 27 advanced file operations

## 27. Advanced File Operations

