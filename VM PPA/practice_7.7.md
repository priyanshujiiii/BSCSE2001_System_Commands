To solve this problem, you need to write a bash script that checks if the number passed as an argument is prime or not. A prime number is a number greater than 1 that has no divisors other than 1 and itself.

Here's a bash script (`script.sh`) to check if a number is prime:

```bash
#!/bin/bash

# Get the input number
n=$1

# Check if the number is less than 2 (since primes are greater than 1)
if [ $n -le 1 ]; then
    echo "Not Prime"
    exit 1
fi

# Check for factors other than 1 and the number itself
for ((i = 2; i * i <= n; i++))
do
    if [ $((n % i)) -eq 0 ]; then
        echo "Not Prime"
        exit 0
    fi
done

# If no factors found, it's a prime number
echo "Prime"
```

### Explanation of the script:
1. **Input Argument**: The script takes an integer `n` as input (`n=$1`).
2. **Prime Number Condition**: If `n` is less than or equal to 1, it immediately outputs "Not Prime" (since prime numbers are greater than 1).
3. **Divisibility Check**: The loop runs from 2 to the square root of `n` (i.e., `i * i <= n`). If `n` is divisible by any number in this range, it's not a prime number, and the script prints "Not Prime" and exits.
4. **Prime Check**: If no divisors are found, the script prints "Prime".

### Example Usage:

1. If you run the script with `n=7`:
   ```bash
   $ ./script.sh 7
   Prime
   ```

2. If you run the script with `n=10`:
   ```bash
   $ ./script.sh 10
   Not Prime
   ```

### Edge Cases:
- **n = 1**: Should output "Not Prime".
- **n = 2**: Should output "Prime" (since 2 is the smallest prime number).
- **n = 4**: Should output "Not Prime".

This script will correctly check if a number is prime or not. Let me know if you need further adjustments!
