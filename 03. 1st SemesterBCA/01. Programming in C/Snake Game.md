# Main Code
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <conio.h>
#include <windows.h>

#define WIDTH 30
#define HEIGHT 20
#define MAX_LENGTH 100

typedef struct {
    int x;
    int y;
} Point;

typedef struct {
    Point body[MAX_LENGTH];
    int length;
    int direction;
    int score;
} Snake;

typedef struct {
    Point position;
    int active;
} Food;

// Game variables
Snake snake;
Food food;
int gameOver = 0;
int gamePaused = 0;

// Function declarations
void initializeGame();
void generateFood();
void draw();
int checkSnakeBody(int x, int y);
void update();
void handleInput(char input);
void gameLoop();
void clearScreen();
char getInput();
void sleepMilliseconds(int ms);

// Platform-specific functions
void clearScreen() {
    system("cls");
}

char getInput() {
    if (_kbhit()) {
        return _getch();
    }
    return 0;
}

void sleepMilliseconds(int ms) {
    Sleep(ms);
}

void initializeGame() {
    // Initialize snake
    snake.length = 3;
    snake.direction = 1;
    snake.score = 0;
    
    // Initial snake position
    int startX = WIDTH / 2;
    int startY = HEIGHT / 2;
    
    for (int i = 0; i < snake.length; i++) {
        snake.body[i].x = startX - i;
        snake.body[i].y = startY;
    }
    
    // Initialize food
    food.active = 1;
    generateFood();
}

void generateFood() {
    int validPosition = 0;
    
    while (!validPosition) {
        food.position.x = rand() % (WIDTH - 2) + 1;
        food.position.y = rand() % (HEIGHT - 2) + 1;
        
        validPosition = 1;
        
        // Check if food position overlaps with snake
        for (int i = 0; i < snake.length; i++) {
            if (snake.body[i].x == food.position.x && 
                snake.body[i].y == food.position.y) {
                validPosition = 0;
                break;
            }
        }
    }
    food.active = 1;
}

int checkSnakeBody(int x, int y) {
    for (int i = 1; i < snake.length; i++) {
        if (snake.body[i].x == x && snake.body[i].y == y) {
            return 1;
        }
    }
    return 0;
}

void draw() {
    clearScreen();
    
    // Draw top border
    for (int i = 0; i < WIDTH + 2; i++) {
        printf("#");
    }
    printf("\n");
    
    for (int y = 0; y < HEIGHT; y++) {
        for (int x = 0; x < WIDTH; x++) {
            // Draw left border
            if (x == 0) {
                printf("#");
            }
            
            // Draw snake head
            if (x == snake.body[0].x && y == snake.body[0].y) {
                printf("O");
            }
            // Draw snake body
            else if (checkSnakeBody(x, y)) {
                printf("o");
            }
            // Draw food
            else if (food.active && x == food.position.x && y == food.position.y) {
                printf("F");
            }
            // Draw empty space
            else {
                printf(" ");
            }
            
            // Draw right border
            if (x == WIDTH - 1) {
                printf("#");
            }
        }
        printf("\n");
    }
    
    // Draw bottom border
    for (int i = 0; i < WIDTH + 2; i++) {
        printf("#");
    }
    printf("\n");
    
    // Display score and instructions
    printf("Score: %d\n", snake.score);
    printf("Controls: W=Up, A=Left, S=Down, D=Right, P=Pause, Q=Quit\n");
    if (gamePaused) {
        printf("PAUSED - Press P to resume\n");
    }
}

void update() {
    if (gamePaused) return;
    
    // Move snake body
    for (int i = snake.length - 1; i > 0; i--) {
        snake.body[i] = snake.body[i - 1];
    }
    
    // Move snake head based on direction
    switch (snake.direction) {
        case 0: // Up
            snake.body[0].y--;
            break;
        case 1: // Right
            snake.body[0].x++;
            break;
        case 2: // Down
            snake.body[0].y++;
            break;
        case 3: // Left
            snake.body[0].x--;
            break;
    }
    
    // Check wall collision
    if (snake.body[0].x < 0 || snake.body[0].x >= WIDTH || 
        snake.body[0].y < 0 || snake.body[0].y >= HEIGHT) {
        gameOver = 1;
        return;
    }
    
    // Check self collision
    for (int i = 1; i < snake.length; i++) {
        if (snake.body[0].x == snake.body[i].x && 
            snake.body[0].y == snake.body[i].y) {
            gameOver = 1;
            return;
        }
    }
    
    // Check food collision
    if (snake.body[0].x == food.position.x && 
        snake.body[0].y == food.position.y) {
        snake.length++;
        snake.score += 10;
        
        // Add new segment at the end
        snake.body[snake.length - 1] = snake.body[snake.length - 2];
        
        // Generate new food
        generateFood();
        
        // Speed up game slightly every 50 points
        if (snake.score % 50 == 0) {
            printf("\nSpeed increased!\n");
        }
    }
}

void handleInput(char input) {
    switch (input) {
        case 'w':
        case 'W':
            if (snake.direction != 2) snake.direction = 0;
            break;
        case 'd':
        case 'D':
            if (snake.direction != 3) snake.direction = 1;
            break;
        case 's':
        case 'S':
            if (snake.direction != 0) snake.direction = 2;
            break;
        case 'a':
        case 'A':
            if (snake.direction != 1) snake.direction = 3;
            break;
        case 'p':
        case 'P':
            gamePaused = !gamePaused;
            break;
        case 'q':
        case 'Q':
            gameOver = 1;
            break;
    }
}

void gameLoop() {
    srand(time(NULL));
    initializeGame();
    
    int speed = 100;
    
    while (!gameOver) {
        draw();
        
        // Handle input
        char input = getInput();
        if (input != 0) {
            handleInput(input);
        }
        
        update();
        
        // Adjust speed based on score
        int currentSpeed = speed - (snake.score / 50) * 10;
        if (currentSpeed < 50) currentSpeed = 50;
        
        sleepMilliseconds(currentSpeed);
    }
    
    // Game over screen
    clearScreen();
    printf("================================\n");
    printf("          GAME OVER\n");
    printf("================================\n");
    printf("      Final Score: %d\n", snake.score);
    printf("================================\n");
    printf("Press any key to exit...\n");
    getchar();
}

int main() {
    clearScreen();
    printf("================================\n");
    printf("       SNAKE GAME IN C\n");
    printf("================================\n");
    printf("Instructions:\n");
    printf("1. Use W, A, S, D to control the snake\n");
    printf("2. Eat the food (F) to grow\n");
    printf("3. Don't hit walls or yourself\n");
    printf("4. Press P to pause/resume\n");
    printf("5. Press Q to quit\n");
    printf("\nPress any key to start...\n");
    getchar();
    
    gameLoop();
    
    return 0;
}
```
# **Snake Game in C - Complete Beginner's Guide**
## **Project Structure Overview** 📋

Let me explain what each part does in simple terms:

```
SNAKE GAME STRUCTURE:
├── 📦 INCLUDES (What our program needs)
├── 📐 SETTINGS (Game rules & limits)
├── 🧩 DATA STRUCTURES (How we store game info)
├── 📊 GAME VARIABLES (Current game state)
├── 🔧 FUNCTION DECLARATIONS (List of all tools we'll use)
├── 🎮 GAME FUNCTIONS (The actual tools)
└── 🚀 MAIN PROGRAM (Where everything starts)
```

---

## **Understanding The Code Line-by-Line** 🔍

### **Part 1: The Includes - What Libraries We Need**

```c
#include <stdio.h>    // For input/output (printf, scanf)
#include <stdlib.h>   // For standard functions (rand, system)
#include <time.h>     // For time functions (seeding random numbers)
#include <conio.h>    // For console input (_kbhit, _getch) - Windows only
#include <windows.h>  // For Sleep() function - Windows only
```

**What this means:** We're telling the computer, "We need these toolboxes to make our game work."

---

### **Part 2: Game Settings - Our Rule Book**

```c
#define WIDTH 30      // Game board width (30 squares wide)
#define HEIGHT 20     // Game board height (20 squares tall)
#define MAX_LENGTH 100 // Maximum snake length (can't grow beyond 100)
```

**Think of it like this:** You're setting up a board game. WIDTH and HEIGHT are how big the board is. MAX_LENGTH is the longest the snake can get.

---

### **Part 3: Data Structures - How We Organize Information**

#### **Point Structure (A Single Dot on the Screen)**

```c
typedef struct {
    int x;  // Horizontal position (like column number)
    int y;  // Vertical position (like row number)
} Point;
```

**Real-world example:** If you have a chess board, `x=3, y=5` means "3rd column, 5th row."

#### **Snake Structure (The Whole Snake)**

```c
typedef struct {
    Point body[MAX_LENGTH];  // Array of all snake parts
    int length;              // Current snake length (starts at 3)
    int direction;           // Which way snake is moving (0-3)
    int score;               // Player's score
} Snake;
```

**Visualization:** The snake is like a train:
- `body[0]` = Engine (head)
- `body[1], body[2], ...` = Train cars (body)
- `length` = How many cars in the train
- `direction` = Which track the train is on

#### **Food Structure (What The Snake Eats)**

```c
typedef struct {
    Point position;  // Where the food is on the board
    int active;      // Is there food currently? (1=yes, 0=no)
} Food;
```

---

### **Part 4: Game Variables - The Current Game State**

```c
Snake snake;       // Our snake object
Food food;         // Our food object
int gameOver = 0;  // Is game finished? (0=no, 1=yes)
int gamePaused = 0; // Is game paused? (0=no, 1=yes)
```

**Current game memory:** These variables remember everything happening right now in the game.

---

### **Part 5: Function Declarations - Our Tool List**

```c
// These tell the computer: "We'll use these functions later"
void initializeGame();      // Sets up a new game
void generateFood();        // Creates new food somewhere
void draw();                // Draws everything on screen
int checkSnakeBody(int x, int y); // Checks if position has snake body
void update();              // Updates game state
void handleInput(char input); // Handles player key presses
void gameLoop();            // Main game cycle
void clearScreen();         // Clears the console
char getInput();            // Gets keyboard input
void sleepMilliseconds(int ms); // Pauses for milliseconds
```

**Why declare first?** It's like telling someone, "I have these tools in my toolbox" before actually showing them.

---

### **Part 6: Platform-Specific Functions - Windows Tools**

```c
void clearScreen() {
    system("cls");  // Windows command to clear screen
}

char getInput() {
    if (_kbhit()) {         // Checks: "Did user press a key?"
        return _getch();    // Gets the key that was pressed
    }
    return 0;               // No key was pressed
}

void sleepMilliseconds(int ms) {
    Sleep(ms);  // Pauses the program for 'ms' milliseconds
}
```

**Translation:** These are Windows-specific ways to:
1. Clear the screen
2. Check for keyboard presses
3. Wait/pause the game

---

### **Part 7: Game Initialization - Starting a New Game**

```c
void initializeGame() {
    // Set up the snake
    snake.length = 3;        // Start with 3 parts
    snake.direction = 1;     // Start moving right (1 = right)
    snake.score = 0;         // Start with 0 points
    
    // Put snake in middle of board
    int startX = WIDTH / 2;   // Middle horizontally
    int startY = HEIGHT / 2;  // Middle vertically
    
    // Create the snake body (3 parts in a row)
    for (int i = 0; i < snake.length; i++) {
        snake.body[i].x = startX - i;  // Each part is left of the previous
        snake.body[i].y = startY;      // All on same row
    }
    
    // Set up the first piece of food
    food.active = 1;         // "Yes, there is food"
    generateFood();          // Put food somewhere random
}
```

**What happens here:**
1. Snake starts in middle with 3 parts: `[head][body][tail]`
2. Facing right: `→`
3. Score is 0
4. Food appears somewhere random

---

### **Part 8: Generating Food - Random Placement**

```c
void generateFood() {
    int validPosition = 0;  // Start assuming position is bad
    
    // Keep trying until we find a good spot
    while (!validPosition) {
        // Pick random position (not too close to edges)
        food.position.x = rand() % (WIDTH - 2) + 1;
        food.position.y = rand() % (HEIGHT - 2) + 1;
        
        validPosition = 1;  // Assume this spot is good
        
        // Check: Is food on top of snake?
        for (int i = 0; i < snake.length; i++) {
            if (snake.body[i].x == food.position.x && 
                snake.body[i].y == food.position.y) {
                validPosition = 0;  // Bad spot - try again
                break;
            }
        }
    }
    food.active = 1;  // Food is now active
}
```

**Process:**
```
1. Try random position
2. Check: Is food on snake?
   - Yes → Try another random position
   - No → Place food there
3. Repeat until good spot found
```

---

### **Part 9: Checking Snake Body - Collision Detection**

```c
int checkSnakeBody(int x, int y) {
    // Check all snake parts EXCEPT head (position 0)
    for (int i = 1; i < snake.length; i++) {
        // Is (x,y) the same as this snake part?
        if (snake.body[i].x == x && snake.body[i].y == y) {
            return 1;  // Yes, there's snake body here
        }
    }
    return 0;  // No snake body here
}
```

**Purpose:** This function answers: "Is there snake body at position (x,y)?"

---

### **Part 10: Drawing The Game - Creating The Visuals**

```c
void draw() {
    clearScreen();  // Clear old frame
    
    // Draw top border
    for (int i = 0; i < WIDTH + 2; i++) {
        printf("#");
    }
    printf("\n");
    
    // Draw game area row by row
    for (int y = 0; y < HEIGHT; y++) {
        for (int x = 0; x < WIDTH; x++) {
            // Left border
            if (x == 0) {
                printf("#");
            }
            
            // What to draw at this position?
            if (x == snake.body[0].x && y == snake.body[0].y) {
                printf("O");  // Snake head
            }
            else if (checkSnakeBody(x, y)) {
                printf("o");  // Snake body
            }
            else if (food.active && x == food.position.x && y == food.position.y) {
                printf("F");  // Food
            }
            else {
                printf(" ");  // Empty space
            }
            
            // Right border
            if (x == WIDTH - 1) {
                printf("#");
            }
        }
        printf("\n");
    }
    
    // Draw bottom border
    for (int i = 0; i < WIDTH + 2; i++) {
        printf("#");
    }
    printf("\n");
    
    // Display game info
    printf("Score: %d\n", snake.score);
    printf("Controls: W=Up, A=Left, S=Down, D=Right, P=Pause, Q=Quit\n");
    if (gamePaused) {
        printf("PAUSED - Press P to resume\n");
    }
}
```

**What gets drawn:**
```
##############################  ← Top border
#          O                 #  ← Snake head
#          o                 #  ← Snake body
#          o      F          #  ← Snake tail & Food
#                            #  ← Empty space
##############################  ← Bottom border
```

---

### **Part 11: Updating Game State - The Game Logic**

```c
void update() {
    if (gamePaused) return;  // Don't update if paused
    
    // MOVE SNAKE BODY: Each part follows the one in front
    for (int i = snake.length - 1; i > 0; i--) {
        snake.body[i] = snake.body[i - 1];
    }
    
    // MOVE SNAKE HEAD based on direction
    switch (snake.direction) {
        case 0: snake.body[0].y--; break; // Up (decrease y)
        case 1: snake.body[0].x++; break; // Right (increase x)
        case 2: snake.body[0].y++; break; // Down (increase y)
        case 3: snake.body[0].x--; break; // Left (decrease x)
    }
    
    // CHECK COLLISIONS
    
    // 1. Wall collision?
    if (snake.body[0].x < 0 || snake.body[0].x >= WIDTH || 
        snake.body[0].y < 0 || snake.body[0].y >= HEIGHT) {
        gameOver = 1;  // Hit wall → Game Over
        return;
    }
    
    // 2. Self collision? (Head hitting body)
    for (int i = 1; i < snake.length; i++) {
        if (snake.body[0].x == snake.body[i].x && 
            snake.body[0].y == snake.body[i].y) {
            gameOver = 1;  // Hit self → Game Over
            return;
        }
    }
    
    // 3. Food collision? (Head hitting food)
    if (snake.body[0].x == food.position.x && 
        snake.body[0].y == food.position.y) {
        
        snake.length++;     // Snake grows by 1
        snake.score += 10;  // Add 10 points
        
        // Add new tail segment (copy last segment)
        snake.body[snake.length - 1] = snake.body[snake.length - 2];
        
        // Create new food
        generateFood();
        
        // Speed up slightly every 50 points
        if (snake.score % 50 == 0) {
            printf("\nSpeed increased!\n");
        }
    }
}
```

**Update Process:**
```
1. Move each body part to where the next one was
2. Move head in current direction
3. Check: Did we hit wall? → Game Over
4. Check: Did we hit ourselves? → Game Over
5. Check: Did we eat food? → Grow & Get Points
```

---

### **Part 12: Handling Input - Player Controls**

```c
void handleInput(char input) {
    switch (input) {
        // Up (can't go down if currently going up)
        case 'w': case 'W':
            if (snake.direction != 2) snake.direction = 0;
            break;
        
        // Right (can't go left if currently going right)
        case 'd': case 'D':
            if (snake.direction != 3) snake.direction = 1;
            break;
        
        // Down (can't go up if currently going down)
        case 's': case 'S':
            if (snake.direction != 0) snake.direction = 2;
            break;
        
        // Left (can't go right if currently going left)
        case 'a': case 'A':
            if (snake.direction != 1) snake.direction = 3;
            break;
        
        // Pause/Resume toggle
        case 'p': case 'P':
            gamePaused = !gamePaused;
            break;
        
        // Quit game
        case 'q': case 'Q':
            gameOver = 1;
            break;
    }
}
```

**Important Rule:** You can't do a 180° turn (can't go up if going down, etc.)

---

### **Part 13: The Game Loop - Heart of the Game**

```c
void gameLoop() {
    srand(time(NULL));      // Seed random number generator
    initializeGame();       // Set up new game
    
    int speed = 100;        // Start speed (100ms delay)
    
    // MAIN GAME LOOP
    while (!gameOver) {     // Keep going until game over
        draw();             // 1. Draw current frame
        
        // 2. Check for player input
        char input = getInput();
        if (input != 0) {
            handleInput(input);
        }
        
        update();           // 3. Update game state
        
        // 4. Control game speed (adjust based on score)
        int currentSpeed = speed - (snake.score / 50) * 10;
        if (currentSpeed < 50) currentSpeed = 50; // Minimum speed
        
        sleepMilliseconds(currentSpeed); // Wait before next frame
    }
    
    // GAME OVER SCREEN
    clearScreen();
    printf("================================\n");
    printf("          GAME OVER\n");
    printf("================================\n");
    printf("      Final Score: %d\n", snake.score);
    printf("================================\n");
    printf("Press any key to exit...\n");
    getchar();
}
```

**Game Loop Cycle (60 times per second approximately):**
```
1. Draw everything
2. Check for keyboard input
3. Update positions & check collisions
4. Wait a little bit
5. Repeat until game over
```

---

### **Part 14: Main Function - Starting Point**

```c
int main() {
    clearScreen();
    
    // Show title screen
    printf("================================\n");
    printf("       SNAKE GAME IN C\n");
    printf("================================\n");
    printf("Instructions:\n");
    printf("1. Use W, A, S, D to control the snake\n");
    printf("2. Eat the food (F) to grow\n");
    printf("3. Don't hit walls or yourself\n");
    printf("4. Press P to pause/resume\n");
    printf("5. Press Q to quit\n");
    printf("\nPress any key to start...\n");
    getchar();  // Wait for key press
    
    gameLoop();  // Start the game
    
    return 0;  // Program ends successfully
}
```

**Program Flow:**
```
main() → Title Screen → gameLoop() → Game Over Screen → Exit
```

---

## **How The Game Works** 🎮

### **The Magic Behind Snake Movement**

Think of the snake as a caterpillar moving:

```
Before moving:   After moving right:
[O][o][o][o]    [ ][O][o][o][o]
Position: 0,1,2,3  Position: _,0,1,2,3 (new head at 4)
```

The trick: We don't actually move each piece forward. Instead:
1. Each piece takes the position of the piece in front of it
2. Only the head actually moves in a new direction

### **Coordinate System Explained**

```
(0,0) ──── (30,0)   ← Top border
   │           │
   │   Game    │
   │   Area    │
   │           │
(0,20) ─── (30,20)  ← Bottom border
```

- `x` increases as you go RIGHT
- `y` increases as you go DOWN
- Snake starts at (15, 10) - middle of 30×20 board

---

## **Game Flow** 📈

```
START
  ↓
Initialize Game
  ├── Create snake (length=3, middle of board)
  └── Generate first food
  ↓
Game Loop (60 FPS)
  ├── Draw Frame
  │   ├── Clear screen
  │   ├── Draw borders
  │   ├── Draw snake
  │   ├── Draw food
  │   └── Draw score
  │
  ├── Get Input
  │   └── Update direction if key pressed
  │
  ├── Update Game
  │   ├── Move snake
  │   ├── Check collisions
  │   │   ├── Wall? → Game Over
  │   │   ├── Self? → Game Over
  │   │   └── Food? → Grow & Score
  │   └── Generate new food if eaten
  │
  └── Wait (Control Speed)
  ↓
Game Over Screen
  ↓
EXIT
```

---

## **Compilation & Running** ⚙️

### **Step-by-Step Compilation:**

```bash
# 1. Save the code as "snake.c"

# 2. Open Command Prompt/PowerShell/Terminal

# 3. Navigate to where you saved the file:
cd "e:\Downloads\Learn Lessons\"

# 4. Compile the code:
gcc snake.c -o snake.exe

# 5. Run the game:
.\snake.exe
```

### **If you get errors:**

1. **"conio.h not found"**: You're not on Windows. Use the Linux version instead.
2. **"undefined reference"**: Make sure you're using Windows and have proper compiler.

---

## **Customization Guide** 🛠️

### **Easy Changes:**

```c
// Change game speed (higher = slower)
int speed = 150;  // Instead of 100

// Change starting length
snake.length = 5;  // Start with longer snake

// Change score per food
snake.score += 20;  // Instead of 10

// Change board size
#define WIDTH 40    // Wider board
#define HEIGHT 30   // Taller board
```

### **Change Snake/Food Characters:**

```c
// In draw() function, change:
printf("@");  // Instead of "O" for head
printf("*");  // Instead of "o" for body
printf("$");  // Instead of "F" for food
```

### **Add Features (For Later):**

1. **High Score**: Save score to file
2. **Different Food Types**: Some give more points
3. **Obstacles**: Walls in middle of board
4. **Levels**: Speed increases every 5 foods
5. **Colors**: Use Windows color functions

---

## **Common Concepts Explained** 📚

### **1. What are `struct`s?**
Think of a `struct` as a "form" or "template". It groups related information together.

**Example:** A "Student" struct:
```c
struct Student {
    char name[50];
    int age;
    float grade;
};
```

### **2. What's `typedef`?**
It creates a shortcut name. Instead of writing `struct Snake` everywhere, we can just write `Snake`.

### **3. Arrays Explained**
```c
Point body[100];  // Creates 100 Point spaces in memory
// body[0] = first Point
// body[1] = second Point
// ...
// body[99] = last Point
```

### **4. Random Numbers**
```c
rand() % 10  // Gives number 0-9
rand() % 20 + 1  // Gives number 1-20
```

### **5. Game Loop Concept**
Games work like flipbooks:
```
Frame 1: Snake at position A
Frame 2: Snake at position B (slightly moved)
Frame 3: Snake at position C (slightly moved)
...
60 frames per second = animation!
```

---

## **Learning Path** 🚀

### **What to Learn Next:**

1. **C Basics** (if you haven't):
   - Variables & Data Types
   - Loops (for, while)
   - Functions
   - Arrays

2. **Game Programming Concepts**:
   - Game loops
   - Collision detection
   - State machines
   - Frame rate control

3. **Advanced C**:
   - Pointers
   - Dynamic memory allocation
   - File I/O (for saving scores)

### **Practice Ideas:**

1. Modify this game to add:
   - A start menu
   - Difficulty levels
   - Sound effects (beeps)
   - High score tracking

2. Create similar games:
   - Pong (simpler)
   - Tetris (more complex)
   - Space Invaders (medium)

---

## **Troubleshooting** 🔧

### **Common Issues:**

1. **Game runs too fast/slow**: Adjust the `speed` variable in `gameLoop()`
2. **Controls not responding**: Make sure Caps Lock is off, use WASD keys
3. **Snake disappears**: Check wall collision logic
4. **Food spawns on snake**: The `generateFood()` function should prevent this

### **Debugging Tips:**
- Add `printf` statements to see what's happening
- Test small parts separately
- Draw diagrams of what should happen vs what does happen

---

## **Final Complete Code**

Here's the complete, well-documented code you can compile and run:

```c
/* ============================================
   SNAKE GAME IN C - COMPLETE BEGINNER VERSION
   Author: Your Name
   Date: Today's Date
   Description: A complete Snake game with 
   detailed comments for learning purposes.
   ============================================ */

/* SECTION 1: INCLUDES - LIBRARIES WE NEED */
#include <stdio.h>    // Standard Input/Output (printing, scanning)
#include <stdlib.h>   // Standard Library (random numbers, system commands)
#include <time.h>     // Time functions (for seeding random numbers)
#include <conio.h>    // Console Input/Output (Windows-specific, for keyboard)
#include <windows.h>  // Windows functions (for Sleep() command)

/* SECTION 2: GAME SETTINGS - ADJUST THESE TO CHANGE GAME */
#define WIDTH 30      // How wide the game board is (in characters)
#define HEIGHT 20     // How tall the game board is (in characters)
#define MAX_LENGTH 100 // Maximum snake length (prevents infinite growth)

/* SECTION 3: DATA STRUCTURES - HOW WE ORGANIZE GAME DATA */

/* A Point represents one spot on the game board */
typedef struct {
    int x;  // Horizontal position (0 = leftmost, WIDTH-1 = rightmost)
    int y;  // Vertical position (0 = top, HEIGHT-1 = bottom)
} Point;

/* The Snake structure holds all snake-related information */
typedef struct {
    Point body[MAX_LENGTH];  // Array of all snake segment positions
    int length;              // Current number of segments
    int direction;           // 0=up, 1=right, 2=down, 3=left
    int score;               // Player's current score
} Snake;

/* The Food structure holds food information */
typedef struct {
    Point position;  // Where the food is located
    int active;      // 1 = food exists, 0 = no food (eaten)
} Food;

/* SECTION 4: GLOBAL VARIABLES - CURRENT GAME STATE */
Snake snake;       // Create one snake object
Food food;         // Create one food object
int gameOver = 0;  // 0 = game running, 1 = game ended
int gamePaused = 0; // 0 = not paused, 1 = game paused

/* SECTION 5: FUNCTION DECLARATIONS - TELLING C ABOUT OUR FUNCTIONS */
void initializeGame();        // Sets up a new game from scratch
void generateFood();          // Places food in a random empty spot
void draw();                  // Draws the entire game screen
int checkSnakeBody(int x, int y); // Checks if position contains snake body
void update();                // Updates all game logic (movement, collisions)
void handleInput(char input); // Processes keyboard input
void gameLoop();              // Main game cycle that runs continuously
void clearScreen();           // Clears the console screen
char getInput();              // Checks for and gets keyboard input
void sleepMilliseconds(int ms); // Pauses execution for given milliseconds

/* SECTION 6: PLATFORM-SPECIFIC FUNCTIONS (WINDOWS VERSION) */

/* Clears the console screen */
void clearScreen() {
    system("cls");  // Windows command: "clear screen"
}

/* Checks if a key was pressed and returns it */
char getInput() {
    if (_kbhit()) {         // _kbhit() checks: "Was a key pressed?"
        return _getch();    // _getch() gets the key that was pressed
    }
    return 0;               // Return 0 if no key was pressed
}

/* Pauses the program for a specified number of milliseconds */
void sleepMilliseconds(int ms) {
    Sleep(ms);  // Windows Sleep() function (ms = milliseconds)
}

/* SECTION 7: GAME INITIALIZATION - SETTING UP A NEW GAME */

/* This function resets all game variables to start a fresh game */
void initializeGame() {
    /* Initialize the snake */
    snake.length = 3;        // Start with 3 segments (head + 2 body)
    snake.direction = 1;     // Start moving right (0=up,1=right,2=down,3=left)
    snake.score = 0;         // Start with zero points
    
    /* Calculate starting position (center of board) */
    int startX = WIDTH / 2;   // Middle column
    int startY = HEIGHT / 2;  // Middle row
    
    /* Create initial snake positions (horizontal line facing right) */
    for (int i = 0; i < snake.length; i++) {
        snake.body[i].x = startX - i;  // Each segment is left of previous
        snake.body[i].y = startY;      // All segments on same row
    }
    
    /* Initialize food */
    food.active = 1;         // Yes, we want food on the board
    generateFood();          // Place the first food piece
}

/* SECTION 8: FOOD GENERATION - PLACING FOOD RANDOMLY */

/* Generates food in a random empty position on the board */
void generateFood() {
    int validPosition = 0;  // Start by assuming position is invalid
    
    /* Keep trying random positions until we find a good one */
    while (!validPosition) {
        /* Generate random coordinates (avoiding edges) */
        food.position.x = rand() % (WIDTH - 2) + 1;   // 1 to WIDTH-2
        food.position.y = rand() % (HEIGHT - 2) + 1;  // 1 to HEIGHT-2
        
        validPosition = 1;  // Temporarily assume this position is good
        
        /* Check if food would overlap with any snake segment */
        for (int i = 0; i < snake.length; i++) {
            if (snake.body[i].x == food.position.x && 
                snake.body[i].y == food.position.y) {
                validPosition = 0;  // Bad position - overlaps with snake
                break;              // Exit the loop early
            }
        }
        /* If validPosition is still 1, we found a good spot! */
    }
    food.active = 1;  // Mark food as active (exists on board)
}

/* SECTION 9: SNAKE BODY CHECK - COLLISION DETECTION HELPER */

/* Checks if a given position contains any part of the snake's body
   (excluding the head, which is at position 0) */
int checkSnakeBody(int x, int y) {
    /* Loop through all body segments (starting from 1, not 0) */
    for (int i = 1; i < snake.length; i++) {
        /* If this body segment is at position (x,y) */
        if (snake.body[i].x == x && snake.body[i].y == y) {
            return 1;  // Yes, snake body is here
        }
    }
    return 0;  // No snake body at this position
}

/* SECTION 10: DRAWING FUNCTION - CREATES THE VISUAL DISPLAY */

/* Draws the entire game screen including borders, snake, food, and info */
void draw() {
    clearScreen();  // Start with a clean screen
    
    /* Draw top border (WIDTH+2 to account for side borders) */
    for (int i = 0; i < WIDTH + 2; i++) {
        printf("#");  # is our border character
    }
    printf("\n");  // Move to next line
    
    /* Draw each row of the game area */
    for (int y = 0; y < HEIGHT; y++) {
        /* Draw each column in this row */
        for (int x = 0; x < WIDTH; x++) {
            /* Draw left border */
            if (x == 0) {
                printf("#");
            }
            
            /* Decide what to draw at this (x,y) position */
            if (x == snake.body[0].x && y == snake.body[0].y) {
                printf("O");  // Snake head
            }
            else if (checkSnakeBody(x, y)) {
                printf("o");  // Snake body
            }
            else if (food.active && x == food.position.x && y == food.position.y) {
                printf("F");  // Food
            }
            else {
                printf(" ");  // Empty space
            }
            
            /* Draw right border */
            if (x == WIDTH - 1) {
                printf("#");
            }
        }
        printf("\n");  // End of this row
    }
    
    /* Draw bottom border */
    for (int i = 0; i < WIDTH + 2; i++) {
        printf("#");
    }
    printf("\n");
    
    /* Display game information below the game board */
    printf("Score: %d\n", snake.score);
    printf("Controls: W=Up, A=Left, S=Down, D=Right, P=Pause, Q=Quit\n");
    if (gamePaused) {
        printf("PAUSED - Press P to resume\n");
    }
}

/* SECTION 11: UPDATE FUNCTION - GAME LOGIC AND RULES */

/* Updates all game state: movement, collisions, scoring */
void update() {
    /* If game is paused, don't update anything */
    if (gamePaused) return;
    
    /* MOVE SNAKE: Each segment takes the position of the one before it */
    for (int i = snake.length - 1; i > 0; i--) {
        snake.body[i] = snake.body[i - 1];  // Body follows head
    }
    
    /* MOVE HEAD: Move head in current direction */
    switch (snake.direction) {
        case 0:  // Up (decrease y coordinate)
            snake.body[0].y--;
            break;
        case 1:  // Right (increase x coordinate)
            snake.body[0].x++;
            break;
        case 2:  // Down (increase y coordinate)
            snake.body[0].y++;
            break;
        case 3:  // Left (decrease x coordinate)
            snake.body[0].x--;
            break;
    }
    
    /* COLLISION DETECTION: Check for wall collisions */
    if (snake.body[0].x < 0 || snake.body[0].x >= WIDTH || 
        snake.body[0].y < 0 || snake.body[0].y >= HEIGHT) {
        gameOver = 1;  // Snake hit wall - game over
        return;        // Exit function early
    }
    
    /* COLLISION DETECTION: Check for self-collision */
    for (int i = 1; i < snake.length; i++) {
        if (snake.body[0].x == snake.body[i].x && 
            snake.body[0].y == snake.body[i].y) {
            gameOver = 1;  // Snake hit itself - game over
            return;        // Exit function early
        }
    }
    
    /* COLLISION DETECTION: Check if snake ate food */
    if (snake.body[0].x == food.position.x && 
        snake.body[0].y == food.position.y) {
        /* SNAKE GROWS: Increase length and score */
        snake.length++;      // Snake gets one segment longer
        snake.score += 10;   // Player gets 10 points
        
        /* Add new segment at the end (copy last segment's position) */
        snake.body[snake.length - 1] = snake.body[snake.length - 2];
        
        /* Generate new food in a different location */
        generateFood();
        
        /* INCREASE DIFFICULTY: Every 50 points, game speeds up */
        if (snake.score % 50 == 0) {
            printf("\nSpeed increased!\n");  // Notify player
        }
    }
}

/* SECTION 12: INPUT HANDLING - PROCESSING PLAYER COMMANDS */

/* Takes a keyboard character and performs the appropriate action */
void handleInput(char input) {
    /* Convert input to appropriate action */
    switch (input) {
        /* UP: 'W' or 'w' key */
        case 'w': case 'W':
            /* Prevent 180-degree turns (can't go up if going down) */
            if (snake.direction != 2) snake.direction = 0;
            break;
        
        /* RIGHT: 'D' or 'd' key */
        case 'd': case 'D':
            /* Can't go right if currently going left */
            if (snake.direction != 3) snake.direction = 1;
            break;
        
        /* DOWN: 'S' or 's' key */
        case 's': case 'S':
            /* Can't go down if currently going up */
            if (snake.direction != 0) snake.direction = 2;
            break;
        
        /* LEFT: 'A' or 'a' key */
        case 'a': case 'A':
            /* Can't go left if currently going right */
            if (snake.direction != 1) snake.direction = 3;
            break;
        
        /* PAUSE/RESUME: 'P' or 'p' key */
        case 'p': case 'P':
            gamePaused = !gamePaused;  // Toggle pause state
            break;
        
        /* QUIT: 'Q' or 'q' key */
        case 'q': case 'Q':
            gameOver = 1;  // End the game
            break;
    }