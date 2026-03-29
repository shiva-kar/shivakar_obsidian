# Reverse Linked List

## Problem
Reverse a singly linked list in-place.

## Approach
Use three pointers: `prev`, `curr`, `next`.

## Code Pattern
```c
Node* reverse(Node* head) {
    Node* prev = NULL;
    Node* curr = head;
    while (curr) {
        Node* next = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next;
    }
    return prev;
}
```

## Mistake
Forgetting to save `next` before rewiring `curr->next`.

## Complexity
Time: O(n)
Space: O(1)

## Related
- [[../../1. Concepts/C/pointers]]
- [[../../1. Concepts/C/structs]]


## Related Concepts
- [[../../1. Concepts/DSA/linked_list]]
- [[../../1. Concepts/C/pointers]]

