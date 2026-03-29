### 37.1 Simple Encryption Algorithms
```c
#include <stdio.h>
#include <string.h>
#include <stdint.h>

// XOR cipher (simple but insecure)
void xor_cipher(const uint8_t *input, uint8_t *output, size_t length, uint8_t key) {
    for (size_t i = 0; i < length; i++) {
        output[i] = input[i] ^ key;
    }
}

// Caesar cipher
void caesar_cipher(char *text, int shift) {
    for (int i = 0; text[i] != '\0'; i++) {
        if (text[i] >= 'A' && text[i] <= 'Z') {
            text[i] = 'A' + (text[i] - 'A' + shift) % 26;
        } else if (text[i] >= 'a' && text[i] <= 'z') {
            text[i] = 'a' + (text[i] - 'a' + shift) % 26;
        }
    }
}

// Simple hash function (FNV-1a)
uint32_t fnv1a_hash(const void *data, size_t length) {
    const uint8_t *bytes = (const uint8_t*)data;
    uint32_t hash = 2166136261u;  // FNV offset basis
    
    for (size_t i = 0; i < length; i++) {
        hash ^= bytes[i];
        hash *= 16777619u;  // FNV prime
    }
    
    return hash;
}

int main() {
    char message[] = "Hello, World!";
    uint8_t encrypted[sizeof(message)];
    
    printf("Original: %s\n", message);
    
    // XOR encryption
    xor_cipher((uint8_t*)message, encrypted, strlen(message), 0xAA);
    printf("XOR Encrypted: ");
    for (size_t i = 0; i < strlen(message); i++) {
        printf("%02X ", encrypted[i]);
    }
    printf("\n");
    
    // Caesar cipher
    caesar_cipher(message, 3);
    printf("Caesar Encrypted: %s\n", message);
    
    // Hash
    uint32_t hash = fnv1a_hash(message, strlen(message));
    printf("Hash: 0x%08X\n", hash);
    
    return 0;
}
```