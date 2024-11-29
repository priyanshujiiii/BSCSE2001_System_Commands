### Concept

To compute the sum of investment amounts for specific investors identified by their hash values:
1. Use the `map` file to associate hash values with the corresponding files in the `data` directory.
2. Filter out only the hash values present in the `result` file.
3. Extract the investment amounts from the corresponding data files.
4. Calculate and output the total sum of the extracted amounts.

---

### Question

**Write a Bash script (`investment.sh`) to calculate the total investment amount for the investors whose hash values are listed in the `result` file.**

#### **Files and Structure**
- **`data`**: Directory containing files with investment details.
- **`map`**: File mapping hash values to `data` file paths.
- **`result`**: File containing the hash values of the selected investors.
  
#### **Expected Output**
For the provided data, the script should print:
```
35245
```

---

### Methodology

1. **Parse the `result` file**:
   Read hash values from `result`.

2. **Map hash values to file paths**:
   Use the `map` file to identify the corresponding file paths for the hashes.

3. **Extract investments**:
   For each mapped file, extract the investment amount using `grep` or similar.

4. **Sum the amounts**:
   Add the extracted investment values.

---

### Script: `investment.sh`

```bash
#!/bin/bash

# Initialize total sum to zero
total_investment=0

# Loop through each hash value in the result file
while read -r hash; do
    # Find the corresponding file path from the map file
    file_path=$(grep "$hash" map | awk '{print $2}')
    
    # Extract the investment amount from the file
    investment=$(grep "INVESTMENT" "$file_path" | awk '{print $2}' | tr -d '$')
    
    # Add the investment to the total sum
    total_investment=$((total_investment + investment))
done < result

# Print the total investment sum
echo "$total_investment"
```

---

### Explanation

1. **`while read -r hash`**: Reads each hash value from the `result` file.
2. **`grep "$hash" map | awk '{print $2}'`**: Finds the file path for the given hash from the `map` file.
3. **`grep "INVESTMENT" "$file_path" | awk '{print $2}' | tr -d '$'`**: Extracts the investment value, removing the `$` symbol.
4. **`total_investment=$((total_investment + investment))`**: Accumulates the extracted values.
5. **`echo "$total_investment"`**: Outputs the final sum.

---

### Output for Provided Data

```bash
$ bash investment.sh
35245
```
