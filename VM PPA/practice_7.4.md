To solve this problem, you'll need to create a bash script that checks the existence and readability of a file given as an argument. The script should handle the following cases:

1. **File does not exist**: Print `"DOES NOT EXIST"` to STDERR and return with exit code 1.
2. **File exists but is not readable**: Print `"NOT READABLE"` to STDERR and return with exit code 2.
3. **File exists and is readable**: Print `"WOO HOO"`.

Here is a solution that uses the provided `if` and `elif` structure for conditional checking:

### **Script (`script.sh`)**:

```bash
#!/bin/bash

# Get the file path from the argument
file_path=$1

# Check if the file exists
if [ ! -e "$file_path" ]; then
    # If the file doesn't exist, print error message to STDERR and exit with code 1
    echo "DOES NOT EXIST" >&2
    exit 1
elif [ ! -r "$file_path" ]; then
    # If the file exists but is not readable, print error message to STDERR and exit with code 2
    echo "NOT READABLE" >&2
    exit 2
else
    # If the file exists and is readable, print the success message
    echo "WOO HOO"
fi
```

### **Explanation:**

1. **`if [ ! -e "$file_path" ]`**:
   - This checks if the file does not exist. The `! -e` condition tests for the absence of the file.
   
2. **`elif [ ! -r "$file_path" ]`**:
   - If the file exists but is not readable, it will check if the file is not readable using `! -r`, which returns true if the file is not readable by the user.

3. **`else`**:
   - If the file exists and is readable, it simply prints `"WOO HOO"`.

4. **`echo "message" >&2`**:
   - This directs the message to **stderr** using `>&2`.

5. **Exit Codes**:
   - The script uses `exit 1` and `exit 2` to indicate specific errors when conditions are not met.

### **Example Usage**:

1. **When the file doesn't exist**:
   ```bash
   $ bash script.sh non_existent_file.txt
   DOES NOT EXIST
   $ echo $?
   1
   ```

2. **When the file exists but is not readable**:
   ```bash
   $ bash script.sh unreadable_file.txt
   NOT READABLE
   $ echo $?
   2
   ```

3. **When the file exists and is readable**:
   ```bash
   $ bash script.sh readable_file.txt
   WOO HOO
   ```

### **Testing**:
- You can create files to test this script:
  - Use `touch` to create a new empty file.
  - Use `chmod` to adjust the readability of a file (e.g., `chmod -r readable_file.txt` to make a file unreadable).

This script meets the problem requirements and handles all the specified cases correctly.
