# Bugs Log

## [C] Segmentation Fault

Mistake:
-> Dereferenced a freed or uninitialized pointer.

Reason:
-> Pointer lifetime was not tracked after `free` and initialization was skipped.

Fix:
-> Initialize to `NULL`, free once, and set pointer to `NULL` after free.

Lesson:
-> Memory safety is a workflow, not a one-time check.

## [C] File Handle Leak

Mistake:
-> Opened files in branches without guaranteed close.

Reason:
-> Early returns bypassed cleanup.

Fix:
-> Use single-exit cleanup style and always `fclose`.

Lesson:
-> Every resource acquisition must have an explicit release path.

## [C] Buffer Overflow

Mistake:
-> Copied user input without bounds checks.

Reason:
-> Assumed input size would fit destination buffer.

Fix:
-> Use bounded APIs (`fgets`, length checks) and reserve null terminator.

Lesson:
-> Trust boundaries matter; validate all external input.
