# LeetCode 3550 — Smallest Index With Digit Sum Equal to Index

## 📌 Problem

Given an integer array `nums`, find the **smallest index `i`** such that the **sum of the digits of `nums[i]` is equal to `i`**.

If no such index exists, return `-1`.

---

## 📝 Examples

### Example 1

```text
Input: nums = [1, 3, 2]
```

Check each index:

```text
Index:  0   1   2
Value:  1   3   2
```

* Index `0`: digit sum of `1` = `1` → `1 != 0` ❌
* Index `1`: digit sum of `3` = `3` → `3 != 1` ❌
* Index `2`: digit sum of `2` = `2` → `2 == 2` ✅

```text
Output: 2
```

---

### Example 2

```text
Input: nums = [1, 10, 11]
```

* Index `0`: digit sum = `1` → `1 != 0` ❌
* Index `1`: digit sum of `10` = `1 + 0 = 1` → `1 == 1` ✅

We return immediately because we need the **smallest index**.

```text
Output: 1
```

Although index `2` also works:

```text
11 → 1 + 1 = 2
```

we don't reach it because index `1` is already a valid answer.

---

### Example 3

```text
Input: nums = [1, 2, 3]
```

* Index `0`: `1 != 0` ❌
* Index `1`: `2 != 1` ❌
* Index `2`: `3 != 2` ❌

No index satisfies the condition.

```text
Output: -1
```

---

## 💡 Approach

The solution is simple:

1. Start from index `0`.
2. Take `nums[i]`.
3. Calculate the sum of its digits.
4. Compare the digit sum with index `i`.
5. If they are equal, return `i`.
6. If no index matches, return `-1`.

Because we check indexes from left to right, the **first matching index is automatically the smallest index**.

---

## 🔢 How to Calculate Digit Sum

For a number like:

```text
123
```

We need:

```text
1 + 2 + 3 = 6
```

We use two important operations:

### `% 10` → Get the last digit

```text
123 % 10 = 3
```

So `% 10` gives the last digit.

### `// 10` → Remove the last digit

```text
123 // 10 = 12
```

So `// 10` removes the last digit.

### Example

For `123`:

```text
123 % 10 = 3
123 // 10 = 12

12 % 10 = 2
12 // 10 = 1

1 % 10 = 1
1 // 10 = 0
```

Therefore:

```text
3 + 2 + 1 = 6
```

### 🧠 Easy Memory Trick

```text
% 10  → TAKE the last digit
// 10 → REMOVE the last digit
```

Think:

```text
TAKE → ADD → REMOVE → REPEAT
```

---

## 🐍 Python Solution

```python
class Solution:
    def smallestIndex(self, nums):
        for i in range(len(nums)):
            n = nums[i]
            digit_sum = 0

            while n > 0:
                digit_sum += n % 10
                n //= 10

            if digit_sum == i:
                return i

        return -1
```

---

## 🔍 Code Explanation

### Step 1 — Loop through every index

```python
for i in range(len(nums)):
```

This checks:

```text
0 → 1 → 2 → 3 → ...
```

---

### Step 2 — Get the current number

```python
n = nums[i]
```

For example:

```text
i = 1
nums[1] = 10

n = 10
```

---

### Step 3 — Start the digit sum

```python
digit_sum = 0
```

We start with zero and keep adding each digit.

---

### Step 4 — Extract every digit

```python
while n > 0:
    digit_sum += n % 10
    n //= 10
```

For `n = 10`:

```text
10 % 10 = 0
digit_sum = 0

10 // 10 = 1

1 % 10 = 1
digit_sum = 1

1 // 10 = 0
```

Final digit sum:

```text
1
```

---

### Step 5 — Compare with the index

```python
if digit_sum == i:
    return i
```

If:

```text
digit_sum = 1
i = 1
```

then:

```text
1 == 1 ✅
```

So we return:

```text
1
```

---

### Step 6 — No match

```python
return -1
```

If every index is checked and none satisfies the condition, return `-1`.

---

## ⏱️ Complexity

Let `n` be the length of the array.

### Time Complexity

```text
O(n × d)
```

where `d` is the number of digits in each number.

Since `nums[i] <= 1000`, there are at most 4 digits, so this is effectively:

```text
O(n)
```

### Space Complexity

```text
O(1)
```

Only a few variables are used.

---

## 🧠 Quick Revision

```text
FOR every index i
       ↓
Take nums[i]
       ↓
Find digit sum
       ↓
digit_sum == i ?
       ↓
YES → return i
NO  → continue
       ↓
No match → return -1
```

### Most Important Trick

```text
n % 10  → last digit
n // 10 → remove last digit
```

**Pattern to remember:**

> Take the last digit → add it → remove it → repeat → compare the sum with the index.
