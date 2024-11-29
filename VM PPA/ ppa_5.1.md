
### **Concept**

This task involves using **Bash scripting** to process files and extract information based on matching hash values. The goal is to calculate the sum of investment amounts for certain investors, as identified by hash values in a `result` file. The key concepts covered are:

- **File Parsing**: Using tools like `grep` to extract specific lines from files.
- **Pattern Matching**: Relating hash values in one file to corresponding records in another.
- **Arithmetic Operations**: Summing up extracted investment values.
- **Scripting**: Automating the task using a Bash script.

---

### **Question**

You are provided with the following data structure:  
- **Files**:
  1. `data/`: Directory containing investor data files.
  2. `map`: File mapping hash values to investor file paths.
  3. `result`: File containing the hash values of selected investors.

**Objective**:  
Write a Bash script `investment.sh` to calculate the total investment amount for investors whose hash values are listed in the `result` file.

**Expected Output**:  
The script should output the sum of the investment amounts of the relevant investors. For the given data, the output is `35245`.

---

### **Methodology**

1. **Parse the `result` file**:
   - Extract all hash values of interest.

2. **Match hashes to file paths**:
   - Use the `map` file to find which files in the `data` directory correspond to these hashes.

3. **Extract investment amounts**:
   - Use `grep` to find the `INVESTMENT` lines in the identified files.

4. **Sum the investments**:
   - Parse and add the extracted investment values.

5. **Print the result**:
   - Display the total investment amount.

---

### **Answer**

Here’s the Bash script `investment.sh`:

```bash
#!/bin/bash

# Initialize total investment variable
total=0

# Loop through each hash in the result file
while read -r hash; do
    # Find the corresponding file path in the map file
    filepath=$(grep "$hash" map | awk '{print $2}')
    
    # Extract the investment amount from the file
    amount=$(grep "INVESTMENT" "$filepath" | awk '{print $2}' | tr -d '$')
    
    # Add the amount to the total
    total=$((total + amount))
done < result

# Print the total investment
echo "$total"
```

---

### **Explanation of the Script**

1. **Initialization**:
   - `total=0`: Variable to store the running total of investments.

2. **Read the `result` file**:
   - `while read -r hash`: Reads each line (hash value) from the `result` file.

3. **Find the file path**:
   - `grep "$hash" map | awk '{print $2}'`: Searches for the hash in the `map` file and extracts the corresponding file path.

4. **Extract the investment amount**:
   - `grep "INVESTMENT" "$filepath" | awk '{print $2}'`: Searches for the investment line in the file and extracts the dollar amount.
   - `tr -d '$'`: Removes the `$` symbol from the amount.

5. **Calculate the total**:
   - `total=$((total + amount))`: Adds the investment amount to the total.

6. **Output the result**:
   - `echo "$total"`: Prints the final sum.

---

### **Execution**

1. Make the script executable:
   ```bash
   chmod +x investment.sh
   ```

2. Run the script:
   ```bash
   ./investment.sh
   ```

3. Output:
   ```bash
   35245
   ```

This script uses efficient file processing commands and ensures the result is computed accurately. Let me know if further clarification is needed!
