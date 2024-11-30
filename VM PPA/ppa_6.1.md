To solve the problem, you need a `sed` script to process `words.txt` by:

1. Swapping the `FIRST` and `second` parts.
2. Converting `FIRST` (uppercase) to lowercase.
3. Converting `second` (lowercase) to uppercase.

### Solution

Here is the content for your `swapcase.sh` script:

```bash
#!/bin/bash

# Use sed to transform the input file
sed -E 's/^([A-Z]+)_([a-z]+)/\U\2_\L\1/' words.txt
```

### Explanation

1. **Regex Breakdown**:
   - `^([A-Z]+)_([a-z]+)`:
     - `^` matches the start of the line.
     - `([A-Z]+)` captures the uppercase word `FIRST`.
     - `_` matches the underscore separating the words.
     - `([a-z]+)` captures the lowercase word `second`.
   - These two groups are captured for swapping.

2. **Replacement Pattern**:
   - `\U\2_\L\1`:
     - `\2` refers to the second group (`second`).
     - `\U\2` converts it to uppercase.
     - `_` adds the underscore.
     - `\1` refers to the first group (`FIRST`).
     - `\L\1` converts it to lowercase.

3. **`-E` Option**:
   - Enables extended regular expressions, simplifying the syntax.

4. **Input File**:
   - `words.txt` is processed directly from the current directory.

### Sample Run

#### Input (`words.txt`):
```text
AD_ux
AD_uy
```

#### Command:
```bash
bash swapcase.sh
```

#### Output:
```text
UX_ad
UY_ad
```

### Making the Script Executable
Run the following commands to test:
```bash
chmod +x swapcase.sh
./swapcase.sh
```
