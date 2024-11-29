### **Conditional Statements, Loops, and Functions in Bash**

Here’s a detailed guide from the basics to advanced levels for **Conditional Statements**, **Loops**, and **Functions** in Bash scripting.

---

## **1. Conditional Statements**

Conditional statements control the flow of your script based on conditions.

### **Basic Syntax**
```bash
if [ condition ]; then
  # Code to execute if condition is true
elif [ another_condition ]; then
  # Code to execute if another_condition is true
else
  # Code to execute if all conditions are false
fi
```

### **Conditions**
Bash uses `test` or `[ ]` to evaluate conditions. Here are common conditions:

#### **Comparison Operators**
- **Numbers:**
  - `-eq` : Equal  
  - `-ne` : Not equal  
  - `-lt` : Less than  
  - `-le` : Less than or equal  
  - `-gt` : Greater than  
  - `-ge` : Greater than or equal  

  Example:
  ```bash
  if [ $num -gt 10 ]; then
    echo "Number is greater than 10"
  fi
  ```

- **Strings:**
  - `=` : Equal  
  - `!=` : Not equal  
  - `-z` : String is empty  
  - `-n` : String is not empty  

  Example:
  ```bash
  if [ "$name" = "John" ]; then
    echo "Hello, John!"
  fi
  ```

- **Files:**
  - `-e` : File exists  
  - `-f` : File exists and is a regular file  
  - `-d` : File exists and is a directory  
  - `-r` : File is readable  
  - `-w` : File is writable  
  - `-x` : File is executable  

  Example:
  ```bash
  if [ -f myfile.txt ]; then
    echo "File exists"
  else
    echo "File does not exist"
  fi
  ```

---

### **Advanced Conditional Statements**
#### **Logical Operators**
- `&&` : AND  
- `||` : OR  

Example:
```bash
if [ $age -gt 18 ] && [ $age -lt 30 ]; then
  echo "You are a young adult"
fi
```

#### **Case Statement**
For matching a variable against multiple patterns:
```bash
case $var in
  pattern1)
    # Code
    ;;
  pattern2)
    # Code
    ;;
  *)
    # Default case
    ;;
esac
```

Example:
```bash
read -p "Enter a color: " color
case $color in
  red) echo "Stop";;
  yellow) echo "Caution";;
  green) echo "Go";;
  *) echo "Invalid color";;
esac
```

---

## **2. Loops**

Loops let you repeat tasks.

### **For Loop**
Basic syntax:
```bash
for variable in list; do
  # Code
done
```

Example:
```bash
for i in 1 2 3 4 5; do
  echo "Number: $i"
done
```

#### **Looping Through Files**
```bash
for file in *.txt; do
  echo "Processing $file"
done
```

---

### **While Loop**
Repeats as long as the condition is true.

Syntax:
```bash
while [ condition ]; do
  # Code
done
```

Example:
```bash
count=1
while [ $count -le 5 ]; do
  echo "Count: $count"
  ((count++))
done
```

---

### **Until Loop**
Repeats until the condition becomes true.

Syntax:
```bash
until [ condition ]; do
  # Code
done
```

Example:
```bash
count=1
until [ $count -gt 5 ]; do
  echo "Count: $count"
  ((count++))
done
```

---

### **Loop Control**
- **Break**: Exit the loop
- **Continue**: Skip to the next iteration

Example:
```bash
for i in {1..5}; do
  if [ $i -eq 3 ]; then
    continue
  fi
  echo $i
done
```

---

### **Nested Loops**
Loops within loops:
```bash
for i in {1..3}; do
  for j in {a..c}; do
    echo "$i$j"
  done
done
```

---

## **3. Functions**

Functions group reusable blocks of code.

### **Basic Syntax**
```bash
function_name() {
  # Code
}
```

### **Examples**
1. **Simple Function**
   ```bash
   greet() {
     echo "Hello, $1!"
   }
   greet "Priyanshu"
   ```

2. **Returning Values**
   ```bash
   add_numbers() {
     local result=$(( $1 + $2 ))
     echo $result
   }
   sum=$(add_numbers 5 10)
   echo "Sum is $sum"
   ```

3. **Function with Conditionals**
   ```bash
   check_even() {
     if [ $(($1 % 2)) -eq 0 ]; then
       echo "$1 is even"
     else
       echo "$1 is odd"
     fi
   }
   check_even 4
   ```

---

### **Advanced Functions**
1. **Using Global and Local Variables**
   ```bash
   calculate() {
     local num=$1
     global_result=$((num * 10))
   }
   calculate 5
   echo "Global result: $global_result"
   ```

2. **Recursive Functions**
   ```bash
   factorial() {
     if [ $1 -le 1 ]; then
       echo 1
     else
       local temp=$(( $1 - 1 ))
       local result=$(factorial $temp)
       echo $(( $1 * result ))
     fi
   }
   echo "Factorial of 5: $(factorial 5)"
   ```

3. **Error Handling**
   ```bash
   divide() {
     if [ $2 -eq 0 ]; then
       echo "Error: Division by zero"
       return 1
     fi
     echo $(( $1 / $2 ))
   }
   divide 10 0
   ```

---

### **Testing and Debugging Tips**
- Add `set -x` at the start of the script to trace execution.
- Use `return` to indicate success or failure in functions.

---

Let me know which specific concept you’d like more examples on!
