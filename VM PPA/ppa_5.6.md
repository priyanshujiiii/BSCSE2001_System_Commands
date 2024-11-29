To solve this problem, we need to extract all unique usernames that successfully logged in (`session opened`) from the log file provided. Here’s how you can achieve this using a shell script:

---

### Implementation

Create a file named `login.sh` with the following content:

```bash
#!/bin/bash
grep "session opened for user" log.txt | awk '{print $9}' | sort | uniq
```

---

### Explanation

1. **`grep "session opened for user"`**:
   - Extracts lines containing the phrase `session opened for user`, which indicates a successful login.

2. **`awk '{print $9}'`**:
   - Extracts the 9th column of the matching lines, which corresponds to the username in the log format.

3. **`sort`**:
   - Sorts the extracted usernames to prepare for removing duplicates.

4. **`uniq`**:
   - Filters out duplicate usernames, leaving only unique ones.

---

### Usage

1. Save the script as `login.sh`.
2. Ensure the script has execution permissions:
   ```bash
   chmod +x login.sh
   ```
3. Run the script:
   ```bash
   ./login.sh
   ```

---

### Input Assumptions

- The log content is saved in a file named `log.txt` in the same directory as `login.sh`.

---

### Sample Output

Given the log content provided, the output will be:
```
guest
guest2
student
```

This matches the sample output in the problem description.
