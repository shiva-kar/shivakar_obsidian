### 22.1 Complex Number Operations
```c
#include <stdio.h>
#include <complex.h>

int main() {
    double complex z1 = 3.0 + 4.0 * I;
    double complex z2 = 1.0 - 2.0 * I;
    
    double complex sum = z1 + z2;
    double complex product = z1 * z2;
    double complex conjugate = conj(z1);
    
    printf("z1 = %.2f + %.2fi\n", creal(z1), cimag(z1));
    printf("z2 = %.2f + %.2fi\n", creal(z2), cimag(z2));
    printf("Sum = %.2f + %.2fi\n", creal(sum), cimag(sum));
    printf("Product = %.2f + %.2fi\n", creal(product), cimag(product));
    printf("Conjugate of z1 = %.2f + %.2fi\n", creal(conjugate), cimag(conjugate));
    printf("Magnitude of z1 = %.2f\n", cabs(z1));
    
    return 0;
}
```