### 24.4 Compilation
```bash
gcc -c math_utils.c -o math_utils.o
gcc -c main.c -o main.o
gcc math_utils.o main.o -o program
./program
```