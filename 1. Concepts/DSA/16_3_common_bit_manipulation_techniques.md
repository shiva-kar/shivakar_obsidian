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