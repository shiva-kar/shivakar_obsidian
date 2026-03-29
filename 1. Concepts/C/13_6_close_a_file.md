### 13.6 Close a File
- `fclose()` closes open file
- Releases system resources
- Flushes any remaining buffer data
- Good practice to set pointer to `NULL` after closing
- Check return value for success (0) or error (EOF)