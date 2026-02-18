# Linked List
## Code C

``` c
#include <stdio.h>      // Provides input/output functions like printf and scanf

#include <stdlib.h>     // Provides memory allocation functions like malloc and free

  

// Define a structure named Node

struct Node {

    int data;               // Integer variable to store the value of the node

    struct Node* next;      // Pointer to the next node in the linked list

};

  

// Function to create a new node dynamically

struct Node* createNode(int value) {

  

    // Allocate memory equal to the size of struct Node

    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));

  

    // Check if memory allocation failed

    if (newNode == NULL) {

        printf("Memory allocation failed\n");  // Print error message

        exit(1);   // Terminate the program immediately with error status

    }

  

    newNode->data = value;   // Store the given value inside the data field

    newNode->next = NULL;    // Initialize next pointer as NULL (no next node yet)

  

    return newNode;          // Return address of the newly created node

}

  

int main() {

  

    struct Node *head = NULL,  // Pointer to first node (initially empty list)

                *temp = NULL,  // Temporary pointer used for traversal

                *newNode = NULL; // Pointer to store newly created node

  

    int n;       // Variable to store number of elements

    int value;   // Variable to store user input value

  

    printf("Enter number of elements: ");   // Ask user for total number of nodes

    scanf("%d", &n);                        // Read integer input and store in n

  

    if (n <= 0) {                           // Check if entered size is invalid

        printf("Invalid size.\n");          // Print error message

        return 0;                           // Exit program normally

    }

  

    for (int i = 0; i < n; i++) {            // Loop runs n times

  

        printf("Enter value %d: ", i + 1);   // Ask user for each value

        scanf("%d", &value);                 // Store input in variable value

  

        newNode = createNode(value);         // Create a new node with input value

  

        if (head == NULL) {                  // If list is empty (first node)

            head = newNode;                  // Make head point to first node

            temp = head;                     // Temp also points to first node

        } else {

            temp->next = newNode;            // Link previous node to new node

            temp = newNode;                  // Move temp pointer to new last node

        }

    }

  

    printf("\nLinked List: ");               // Print heading before displaying list

  

    temp = head;                             // Start traversal from head

  

    while (temp != NULL) {                   // Continue until end of list

        printf("%d ", temp->data);           // Print current node's data

        temp = temp->next;                   // Move to next node

    }

  

    temp = head;                             // Reset temp to head for memory freeing

  

    while (temp != NULL) {                   // Loop until all nodes are freed

        struct Node* nextNode = temp->next;  // Store address of next node

        free(temp);                          // Free memory of current node

        temp = nextNode;                     // Move to next node

    }

  

    return 0;   // Indicate successful execution of program

}
```
