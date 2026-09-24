# LeetCode 3498 — Reverse Degree of a String

## 📌 Problem

Given a string `s`, calculate its **reverse degree**.

For every character:

```text
Reverse alphabet value × Position in the string
```

Then add all the products.

The alphabet is reversed:

```text
a = 26
b = 25
c = 24
...
x = 3
y = 2
z = 1
```

The position of characters in the string is **1-indexed**.

---

## 📝 Example 1

### Input

```text
s = "abc"
```

| Character | Reverse Alphabet Value | Position | Product |
| --------- | ---------------------: | -------: | ------: |
| `a`       |                     26 |        1 |      26 |
| `b`       |                     25 |        2 |      50 |
| `c`       |                     24 |        3 |      72 |

```text
26 + 50 + 72 = 148
```

### Output

```text
148
```

---

## 📝 Example 2

### Input

```text
s = "zaza"
```

| Character | Reverse Alphabet Value | Position | Product |
| --------- | ---------------------: | -------: | ------: |
| `z`       |                      1 |        1 |       1 |
| `a`       |                     26 |        2 |      52 |
| `z`       |                      1 |        3 |       3 |
| `a`       |                     26 |        4 |     104 |

```text
1 + 52 + 3 + 104 = 160
```

### Output

```text
160
```

---

## 💡 Approach

1. Start `answer` with `0`.
2. Loop through every character in the string.
3. Get the current character.
4. Find its reverse alphabet value.
5. Multiply it by its 1-indexed position.
6. Add the result to `answer`.
7. Return `answer`.

---

## 🔢 Finding the Reverse Alphabet Value

Normally:

```text
a = 1
b = 2
c = 3
...
z = 26
```

But we need the reverse:

```text
a = 26
b = 25
c = 24
...
z = 1
```

We can calculate it using:

```python
ord('z') - ord(ch) + 1
```

For example, for `a`:

```text
ord('z') - ord('a') + 1
= 122 - 97 + 1
= 26
```

For `z`:

```text
122 - 122 + 1
= 1
```

---

## 🔍 Understanding `ord()`

Python's `ord()` gives the numerical Unicode value of a character.

```python
ord('a')  # 97
ord('b')  # 98
ord('z')  # 122
```

Therefore:

```python
ord('z') - ord(ch) + 1
```

can calculate the reversed alphabet position.

---

## 🔢 Why `i + 1`?

Python uses **0-based indexing**:

```text
Index:     0   1   2
String:    a   b   c
```

But the problem uses **1-based positions**:

```text
Position:  1   2   3
String:    a   b   c
```

Therefore:

```python
i + 1
```

converts the Python index into the required position.

---

## 🐍 Python Solution

```python
class Solution:
    def reverseDegree(self, s):
        answer = 0

        for i in range(len(s)):
            ch = s[i]
            reverse_value = ord('z') - ord(ch) + 1
            answer += reverse_value * (i + 1)

        return answer
```

---

## 🔍 Code Explanation

### Initialize answer

```python
answer = 0
```

Stores the total reverse degree.

### Loop through the string

```python
for i in range(len(s)):
```

Checks every character using its index.

### Get the character

```python
ch = s[i]
```

For `"abc"`:

```text
i = 0 → a
i = 1 → b
i = 2 → c
```

### Find reverse alphabet value

```python
reverse_value = ord('z') - ord(ch) + 1
```

For `"abc"`:

```text
a → 26
b → 25
c → 24
```

### Calculate and add the product

```python
answer += reverse_value * (i + 1)
```

For `"abc"`:

```text
26 × 1 = 26
25 × 2 = 50
24 × 3 = 72
```

Total:

```text
26 + 50 + 72 = 148
```

### Return the result

```python
return answer
```

---

## 🧠 Easy Memory Trick

Remember:

```text
Character
    ↓
Reverse alphabet value
    ↓
×
    ↓
Position (i + 1)
    ↓
Add to answer
```

### Important Formula

```python
reverse_value = ord('z') - ord(ch) + 1
```

```python
answer += reverse_value * (i + 1)
```

### 🔥 Remember

```text
ord()     → character's numeric value
i + 1     → 1-indexed position
reverse × position → product
```

---

## ⏱️ Complexity

### Time Complexity

```text
O(n)
```

Each character is processed once.

### Space Complexity

```text
O(1)
```

Only a few variables are used.
