# Bugs

## Linked List Segmentation Fault

Mistake:
-> Dereferenced an uninitialized node pointer.

Reason:
-> Pointer variable was declared but never initialized before first use.

Fix:
-> Initialize pointers to `NULL`, allocate before dereference, and guard null checks.

## File Handle Leak

Mistake:
-> Opened files in a loop without closing them.

Reason:
-> Missing `fclose` on early return paths.

Fix:
-> Close handles on all exit paths and centralize cleanup.

## Buffer Overflow in String Copy

Mistake:
-> Used unsafe copy without bounds check.

Reason:
-> Assumed source input length always fits destination.

Fix:
-> Use bounded APIs, validate lengths, and reserve null terminator space.
