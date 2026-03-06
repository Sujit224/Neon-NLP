Regular Expressions (RegEx) are a sequence of characters that form a search pattern. In NLP, before feeding text to complex machine learning models, you must clean and preprocess the raw data. RegEx is your primary tool for **pattern matching, text extraction, and text cleaning**.

## Implementing RegEx

### Using \d
By itself, `\d` only matches **one single digit** at a time.
```python
import re

text = "I bought 3 apples and 12 bananas."

# Find every single digit individually
single_digits = re.findall(r'\d', text)
print(single_digits)
# Output: ['3', '1', '2']
```


```python
import re

text = "Patient ID 8472 was admitted in 2023 and discharged in 2026."

# \d+ matches ONE OR MORE digits in a row (extracts whole numbers)
all_numbers = re.findall(r'\d+', text)
print(all_numbers)
# Output: ['8472', '2023', '2026']

# \d{4} matches EXACTLY FOUR digits in a row (great for years)
years = re.findall(r'\d{4}', text)
print(years)
# Output: ['8472', '2023', '2026']
```

---
### Using ()
The () is used to match everything present in it
It has matched all instances containing 3 digits
![[RegEx_Img2.png]]

---
### Using \ (Escape Character)

RegEx has a lot of "meta-characters" that perform special functions: `.` `*` `+` `?` `[` `]` `(` `)` `{` `}` `^` `$`.
But what if you actually want to find a literal question mark in a sentence? Or a literal period? If you just type `?` or `.`, the RegEx engine will try to execute a command.
To tell the engine "treat this as a normal punctuation mark," you **escape** it by putting a `\` right in front of it.
![[RegEx_Img3.png]]

- **Incorrect Pattern:** `(\d{3})-\d{3}-\d{4}`
    
    - _Result:_ Captures "123" in a group, but expects the text to just say "123-567-8912". It will fail to match `(123)`.
        
- **Correct Pattern:** `\(\d{3}\)-\d{3}-\d{4}`
    
    - _How it works:_ `\(` looks for a literal opening parenthesis. `\d{3}` looks for 3 numbers. `\)` looks for a literal closing parenthesis.
---

### Matching a range of characters using []
![[RegEx_Img4.png]]

---
### Using the ^ operator
![[RegEx_Img5.png]]

---
