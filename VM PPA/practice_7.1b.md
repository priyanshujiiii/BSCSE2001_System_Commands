Here is the solution for the given problem. The script accepts a name as a command-line argument and prints the greeting message.

---

### Implementation (`script.sh`)
```bash
#!/bin/bash

# Check if a name is passed as a command-line argument
if [ $# -eq 0 ]; then
    echo "Usage: $0 <name>"
    exit 1
fi

# Get the name from the first command-line argument
input_name=$1

# Print the greeting message
echo "hello $input_name"
```

---

### Explanation

1. **`if [ $# -eq 0 ]; then`**:
   - This checks if no arguments were provided to the script. If true, it displays a usage message and exits.

2. **`input_name=$1`**:
   - The `$1` variable contains the first argument passed to the script. This is assigned to the variable `input_name`.

3. **`echo "hello $input_name"`**:
   - The `echo` command prints the message, inserting the value of `input_name`.

4. **Error Handling**:
   - If no name is provided, the script outputs a usage message like:
     ```
     Usage: ./script.sh <name>
     ```

---

### Example Usage

#### Input:
```bash
$ bash script.sh Raghu
```

#### Output:
```bash
hello Raghu
```

#### Without an Argument:
```bash
$ bash script.sh
Usage: ./script.sh <name>
``` 

This ensures robust handling of input and outputs the greeting correctly.
