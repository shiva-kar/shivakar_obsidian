# Control Flow

## Core Idea
Control flow decides which code runs and when.

## Why it exists
Programs need decisions and repetition to solve real problems.

## Mental Model
Like traffic routing: conditions choose roads, loops repeat routes.

## Code Pattern
~~~c
for (int i = 0; i < n; i++) {
    if (arr[i] % 2 == 0) continue;
    printf("%d\\n", arr[i]);
}
~~~

## Common Mistakes
- Infinite loops by bad conditions
- Deep nesting reducing readability

## Interview Angle
- while vs for usage
- break/continue behavior

## Related
- [[operators]]
- [[functions]]
- [[arrays]]

## Legacy Notes (archived)
# control flow

Merged from legacy micro-notes.

## 4 1 what is decision control

### 4.1 What is Decision Control?
1. Conditional execution based on conditions
2. Handles complex decisions through nesting
3. Increases program adaptability

## 4 11 goto statement

### 4.11 Goto Statement
- Unconditional jump to label
- Label defined with name and colon
- Must be in same function
- Useful for error handling, nested loop exiting
- Generally discouraged

## 4 2 relational operator

### 4.2 Relational Operator
- `==`: Equality
- `!=`: Inequality
- `>`: Greater than
- `<`: Less than
- `>=`: Greater than or equal
- `<=`: Less than or equal

## 4 3 if statement

### 4.3 if Statement
- Syntax: `if (condition) { }`
- Executes block if condition true
- Curly braces optional for single statements (not recommended)
- Can store conditions in variables

## 4 4 truthy vs falsy

### 4.4 Truthy vs Falsy
- **Falsy**: `0` and `NULL`
- **Truthy**: Any non-zero value
- Used in `if`, `while`, `for` conditions
- Automatic conversion based on numeric value

## 4 5 if else

### 4.5 if-else
- `else` executes when `if` condition is false
- Provides alternative execution path

## 4 6 if else if ladder

### 4.6 if-else-if Ladder
1. Sequential condition checking
2. Executes first true condition's block
3. Exits after finding true condition
4. Final `else` as default case

## 4 7 nested if

### 4.7 Nested if
- `if` inside another `if` or `else`
- Enables hierarchical condition checks
- Allows detailed decision paths
- Deep nesting can redu


## Questions
- When should I use this instead of an alternative?
- What edge case is most likely to break this approach?

