# bit manipulation

## Core Idea
Problem-oriented DSA concept note.

## Typical Problems
- Add canonical problems here.

## Legacy Notes (archived)

### 16 3 common bit manipulation techniques

### 16.3 Common Bit Manipulation Techniques
```c
// Set bit n
x |= (1 << n);

// Clear bit n
x &= ~(1 << n);

// Toggle bit n
x ^= (1 << n);

// Check if bit n is set
if (x & (1 << n)) {
    // Bit is set
}

// Count set bits (Brian Kernighan's algorithm)
int countSetBits(unsigned int n) {
    int count = 0;
    while (n) {
        n &= (n - 1);
        count++;
    }
    return count;
}
```

