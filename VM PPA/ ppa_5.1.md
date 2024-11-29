
### **Concept**

This task involves using **Bash scripting** to process files and extract information based on matching hash values. The goal is to calculate the sum of investment amounts for certain investors, as identified by hash values in a `result` file. The key concepts covered are:

- **File Parsing**: Using tools like `grep` to extract specific lines from files.
- **Pattern Matching**: Relating hash values in one file to corresponding records in another.
- **Arithmetic Operations**: Summing up extracted investment values.
- **Scripting**: Automating the task using a Bash script.

---

### **Question**

# Programming Practice Assignment - Week 5 - Question 2

## Problem Statement

A finance company called `Fintech` does not have its own analytics team, rather they outsources their analytics work to external vendors.
The company maintains a file for each investor they are interested in, with the filename in the format `firstname_lastname` in the directory `data` (directory `data` is in the current working directory).
They do not want to make their investor details public so they rename each investor file to the hash value of filename before giving it to the external vendors and store the mapping in the file named `map`.
Assume that no two investors have same combination of `firstname` and `lastname`.

The analytics team(external vendor) received the files of several investors named as some hash value.
They analysed and identified some potential investors for the company and stored the hashed file names(one on each line) corresponding to the identified investors in a file named `result`.
The `firstname_lastname` file contains the potential investment amount and duration details.
Refer the provided sample data for sample file formats and architecture.

### Architecture and Sample Data

```bash
$ ls -Rl
.:
total 4
drwxrwxrwx 1 user user 512 Dec 11 19:48 data
-rwxrwxrwx 1 user user 435 Dec 11 20:53 map
-rwxrwxrwx 1 user user 195 Dec 11 20:53 result

./data:
total 0
-rwxrwxrwx 1 user user 36 Dec 11 20:53 Billie_Barron
-rwxrwxrwx 1 user user 36 Dec 11 20:53 Jeremiah_Brennan
-rwxrwxrwx 1 user user 36 Dec 11 20:53 Long_Mclaughlin
-rwxrwxrwx 1 user user 35 Dec 11 20:53 Lorna_Trevino
-rwxrwxrwx 1 user user 35 Dec 11 20:53 Mandy_Mueller

$ cat ./data/Billie_Barron
INVESTMENT $16319
FROM 2026
TO 2026

$ cat map
bb1cc74d6e8c40efdbbbc0e6a657fca02a533fe7f438d5b09b47b43e31cb9a45 ./data/Mandy_Mueller
fe818c4ac047523ac14dbb341f365bbfcd857268a6bfb70d9abb701a80bfb9c3 ./data/Lorna_Trevino
e8b80161e4110a791a0d7c3e40a04099fc75f0e348c2033efe79a2a930a71e98 ./data/Long_Mclaughlin
b1b1222a15fcd532e511d0f461dbe7ae7bda825b68bc510eec2a22cbddd5dad2 ./data/Billie_Barron
6051c4f27079a41afc99a97f0fc7bb8ba2789cd282f4cd10a71c6a954089b63e ./data/Jeremiah_Brennan

$ cat result
bb1cc74d6e8c40efdbbbc0e6a657fca02a533fe7f438d5b09b47b43e31cb9a45
fe818c4ac047523ac14dbb341f365bbfcd857268a6bfb70d9abb701a80bfb9c3
e8b80161e4110a791a0d7c3e40a04099fc75f0e348c2033efe79a2a930a71e98

$ grep INVESTMENT -r
data/Billie_Barron:INVESTMENT $16319
data/Jeremiah_Brennan:INVESTMENT $29440
data/Long_Mclaughlin:INVESTMENT $25906
data/Lorna_Trevino:INVESTMENT $1360
data/Mandy_Mueller:INVESTMENT $7979
```

### Expected output for above data

35245

## Instructions

Write a bash script to print the sum of investment amounts of all the investors identified by the analytics team whose names(hash values) are present in the file `result`.

Store your commands in the file `investment.sh`.
Your script will not recieve any input through standard input, or as arguments.
Your script should print output to the standard output.


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
