### 11.5 Structure Initialization
- Direct: `struct Student s1 = {1, "Alice", 85.5};`
- Designated (C99): `struct Student s2 = {.rollno=2, .name="Bob", .marks=90.2};`
- Zero: `struct Student s3 = {0};`
- Copy: `struct Student s4 = s1;`