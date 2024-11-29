### Problem Breakdown

The goal is to write a shell script (`arch.sh`) that extracts the system's processor architecture from the output of the `uname -a` command. The processor architecture typically appears as strings like `x86_64`, `arm64`, etc., in the output.

---

### Solution Concept

1. **Command to Get Architecture**: The `uname -m` command directly provides the processor architecture without needing to parse the full output of `uname -a`. This is more reliable and concise.
2. **Output**: Ensure the output is clean and contains only the processor architecture.

---

### Implementation

Create a file named `arch.sh` with the following content:

```bash
#!/bin/bash
uname -m
```

---

### Explanation

- **`uname -m`**:
  - Outputs the machine hardware name, which corresponds to the processor architecture (e.g., `x86_64`, `arm64`).
- **No Parsing Required**: Since `uname -m` directly gives the desired information, there's no need for further parsing or regex matching.

---

### Usage

1. Make the script executable:
   ```bash
   chmod +x arch.sh
   ```

2. Run the script:
   ```bash
   ./arch.sh
   ```

---

### Sample Output

If the system architecture is `x86_64`:
```
x86_64
```

If the system architecture is `arm64`:
```
arm64
```
