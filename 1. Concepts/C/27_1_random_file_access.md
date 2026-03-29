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