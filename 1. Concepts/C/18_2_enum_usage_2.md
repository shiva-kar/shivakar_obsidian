### 18.2 Enum Usage
```c
#include <stdio.h>

enum TrafficLight { RED, YELLOW, GREEN };

const char* getLightColor(enum TrafficLight light) {
    switch (light) {
        case RED: return "Stop";
        case YELLOW: return "Caution";
        case GREEN: return "Go";
        default: return "Unknown";
    }
}

int main() {
    enum TrafficLight current = RED;
    
    printf("Current light: %s\n", getLightColor(current));
    
    // Iterate through enum values
    for (enum TrafficLight light = RED; light <= GREEN; light++) {
        printf("Light %d: %s\n", light, getLightColor(light));
    }
    
    return 0;
}
```