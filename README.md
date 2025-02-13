# **Luhn Algorithm – Credit Card Validation**  

## **Overview**  

The **Luhn Algorithm**, also known as the **Modulus 10 (mod 10) Algorithm**, is a simple checksum formula used to validate identification numbers such as **credit card numbers, IMEI numbers**, and more. It was developed by **Hans Peter Luhn**, a scientist at IBM, and is widely used for **fraud detection and error prevention**.  

### **How the Luhn Algorithm Works**  

1. **Reverse the Card Number**: Start from the rightmost digit and move left.  
2. **Double Every Second Digit**: If doubling a digit results in a number greater than 9, subtract 9 or sum its digits.  
3. **Sum All Digits**: Add up all the individual digits obtained.  
4. **Check Modulo 10**: If the total sum is divisible by **10**, the card number is valid; otherwise, it’s invalid.  

### **Example Calculation**  

Let’s validate the number **4539 1488 0343 6467**:  

| Step | Digits | Double Every Second? | New Digits | Sum |
|------|--------|----------------------|------------|-----|
| Original | **4 5 3 9 1 4 8 8 0 3 4 3 6 4 6 7** | No | **4 5 3 9 1 4 8 8 0 3 4 3 6 4 6 7** | - |
| Reverse  | **7 6 4 6 3 4 3 0 8 8 4 1 9 3 5 4** | - | - | - |
| Double Every Second | **7 12 4 12 3 8 3 0 16 8 8 1 18 3 10 4** | Yes | **7 3 4 3 3 8 3 0 7 8 8 1 9 3 1 4** | - |
| Sum | **7 + 3 + 4 + 3 + 3 + 8 + 3 + 0 + 7 + 8 + 8 + 1 + 9 + 3 + 1 + 4** | - | **70** | - |
| Check Modulo 10 | **70 % 10 == 0** | - | ✅ Valid Card | - |

---

## **Python Implementation**  

This implementation of the **Luhn Algorithm** validates a given credit card number using Python.  

### **Code Explanation**  

```python
def checkLuhn(cardNo):
    # Get the number of digits in the card number
    nDigits = len(cardNo)
    nSum = 0
    isSecond = False  # Tracks whether the current digit should be doubled

    # Loop through the card number in reverse order
    for i in range(nDigits - 1, -1, -1):
        # Convert character to integer (e.g., '3' -> 3)
        d = ord(cardNo[i]) - ord('0')

        # Double every second digit
        if isSecond:
            d = d * 2

        # If doubling results in a two-digit number, split the digits and sum them
        nSum += d // 10
        nSum += d % 10

        # Alternate the isSecond flag for the next iteration
        isSecond = not isSecond

    # If the total sum is a multiple of 10, the card is valid
    return (nSum % 10 == 0)
```
**Applications of the Luhn Algorithm**  

🔹 **Credit Card Verification** – Used by financial institutions to detect invalid card numbers.  
🔹 **IMEI Number Validation** – Ensures the correctness of mobile device identification numbers.  
🔹 **Government IDs** – Many identification numbers (e.g., Social Security numbers) use Luhn checks.  
🔹 **Error Detection in Data Transmission** – Helps prevent accidental errors in numeric sequences.  
