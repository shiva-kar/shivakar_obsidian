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
- Deep nesting can reduce readability

## 4 8 logical operators

### 4.8 Logical Operators
- `&&`: AND (all conditions must be true)
- `||`: OR (at least one condition true)
- `!`: NOT (inverts condition)
- Lower priority than arithmetic/comparison

## 4 9 ternary operator

### 4.9 Ternary Operator
- Syntax: `condition ? expression1 : expression2`
- Boolean condition evaluation
- Both expressions must return compatible types
- Good for simple assignments

## 4 decision control structure

## 4. Decision Control Structure

## 5 2 while loop

### 5.2 While Loop
- Repeats while condition is true
- Used for non-standard conditions
- Must include update to avoid infinite loops

## 5 3 for loop

### 5.3 For Loop
- Standard loop for counting iterations
- Preferred when number of iterations known
- Syntax: `for (initialization; condition; update)`

## 5 4 break statement

### 5.4 Break Statement
- Stops loop early or breaks out
- Exits loops and switch cases
- Immediate effect
- Alters program flow

## 5 6 odd loop

### 5.6 Odd Loop
- Runs unknown number of times
- Condition-driven
- Uses `while` and `do-while`
- May use `break` for exit
- Design carefully to avoid infinite loops

## 5 7 do while loop

### 5.7 Do-while Loop
- Executes block first, then checks condition
- Guaranteed at least one iteration
- Unlike while, first iteration unconditional
- Update condition to avoid infinite loops

## 5 8 infinite loop

### 5.8 Infinite Loop
- Endless execution
- Purposeful or accidental
- Requires `break` or similar to stop
- May cause high CPU usage

## 5 iteration loop control structure

## 5. Iteration & Loop Control Structure

