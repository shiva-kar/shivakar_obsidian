# Concurrency

## Core Idea
Coordinate multiple execution flows safely.

## Why it exists
Improve responsiveness and throughput.

## Mental Model
Many workers, shared state hazards, explicit synchronization.

## Code Pattern
```c
// pthread_create + mutex pattern
```

## Common Mistakes
- Data races
- Deadlocks

## Interview Angle
- Race condition vs deadlock
- Mutex vs atomics

## Related
- [[../memory_management]]
- [[../functions]]

## Legacy Notes (archived)
- Use `std::filesystem`, `std::thread`, `std::chrono` instead of OS calls.
LDFLAGS = -lm -lpthread


## Questions
- When should I use this instead of an alternative?
- What edge case is most likely to break this approach?

