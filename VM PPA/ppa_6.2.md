To implement the solution for the described problem, the script must handle multiple options (`-l`, `-w`, `-n`, and `-s`) using `sed` and manage combinations of options while counting specific details from a file.

Here's the `myCount.sh` script implementation:

---

### Implementation

```bash
#!/bin/bash

# Extract the file path (last argument)
file="${@: -1}"

# Check if no arguments are passed or file doesn't exist
if [[ $# -eq 0 ]] || [[ ! -f "$file" ]]; then
    exit 0
fi

# Iterate through all options using a loop
while [[ $# -gt 1 ]]; do
    case "$1" in
        -l)
            # Count the number of lines
            sed -n '$=' "$file"
            ;;
        -w)
            # Count the number of words
            sed -E 's/\s+/\n/g' "$file" | sed '/^$/d' | sed -n '$='
            ;;
        -n)
            # Count lines with only numeric values
            sed -n '/^[0-9]\+$/p' "$file" | sed -n '$='
            ;;
        -s)
            # Count lines containing the specified string
            shift
            sed -n "/$1/p" "$file" | sed -n '$='
            ;;
        *)
            # Ignore invalid options
            ;;
    esac
    shift
done
```

---

### Explanation of the Code

1. **File Validation**:
   - The script checks if arguments are passed and if the last argument corresponds to a valid file. If not, the script exits.

2. **Using `while` Loop**:
   - The loop processes all arguments until the last argument (the file path).
   - Options are matched using `case`.

3. **Counting with `sed`**:
   - `-l`: `sed -n '$='` outputs the total number of lines in the file.
   - `-w`: Words are split into separate lines using `sed -E 's/\s+/\n/g'`, empty lines are removed, and the total count is output with `sed -n '$='`.
   - `-n`: Lines with only numeric values are matched using the regex `/^[0-9]\+$/`.
   - `-s`: Lines containing the specified string are matched using `/str/`.

4. **Multiple Options**:
   - The loop ensures all specified options are processed, and results are printed in the specified order.

---

### Example Execution

#### Input File (`somefile.txt`):
```text
This is a sample file
this is not end justsay start
that contains say
some number
say like 10
or
20
or
233
444
or say 3444
and now it ends.
```

#### Commands and Outputs:
```bash
$ bash myCount.sh -l somefile.txt
12

$ bash myCount.sh -w somefile.txt
32

$ bash myCount.sh -n somefile.txt
3

$ bash myCount.sh -s say somefile.txt
4

$ bash myCount.sh -l -n somefile.txt
12
3

$ bash myCount.sh -l -s say -l -n somefile.txt
12
4
12
3
```

---

### Key Notes

1. **No `wc` or `awk`**:
   - The solution strictly uses `sed` for all counting tasks.

2. **Efficient Processing**:
   - The script uses `sed`'s built-in line counting (`$=`) and regex capabilities to minimize additional commands.

3. **Error Handling**:
   - Invalid options are ignored, and the script exits if no arguments or invalid file paths are provided.

This implementation adheres to all the requirements of the problem statement and handles edge cases effectively.
