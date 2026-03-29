### 18.1 Enum Declaration
```c
enum Weekdays {
    MONDAY,    // 0
    TUESDAY,   // 1
    WEDNESDAY, // 2
    THURSDAY,  // 3
    FRIDAY,    // 4
    SATURDAY,  // 5
    SUNDAY     // 6
};

enum Colors {
    RED = 1,
    GREEN = 2,
    BLUE = 4,
    YELLOW = RED | GREEN,  // 3
    WHITE = RED | GREEN | BLUE  // 7
};
```