Here is the solution for the given problem. The script reads a name from `stdin` and prints the greeting message.

---

### Implementation (`script.sh`)
```bash
#!/bin/bash

# Read the input string from stdin
read input_name

# Print the greeting message
echo "hello $input_name"
```

---

### Explanation

1. **`read input_name`**:
   - The `read` command takes input from the user and stores it in the variable `input_name`.

2. **`echo "hello $input_name"`**:
   - The `echo` command prints the message, inserting the value of `input_name` into the output.

---

### Example Usage

#### Input:
```bash
$ bash script.sh
Raghu
```

#### Output:
```bash
hello Raghu
```

This script meets the problem requirements by dynamically generating the greeting message using the provided input.
