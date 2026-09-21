# LeetCode 3524 - Find X Value of Array I

## 🧩 Problem

Given an array `nums` of positive integers and an integer `k`.

We can choose any **non-empty subarray** of `nums` by removing:

* a prefix
* a suffix

The remaining elements must not be empty.

For every possible remainder `x` from `0` to `k - 1`, count how many subarrays have:

```text
(product of elements) % k == x
```

Return the counts as an array of size `k`.

---

## 💡 Simple Idea

We don't need the actual product.

We only care about:

```text
product % k
```

For every starting position, keep track of the possible remainders of subarrays ending at the current position.

### Example

```text
nums = [1, 2, 3]
k = 3
```

For subarray:

```text
[1, 2, 3]
```

Product:

```text
1 × 2 × 3 = 6
```

Remainder:

```text
6 % 3 = 0
```

So we add `1` to:

```text
result[0]
```

---

## 🧠 DP Idea

We use:

```text
dp[r] = number of subarrays ending at the previous position
        whose product % k == r
```

For every new number `num`:

### 1. Start a new subarray

```text
num % k
```

So:

```text
new_dp[num % k] += 1
```

### 2. Extend previous subarrays

If an old subarray had remainder `r`:

```text
new remainder = (r * num) % k
```

So:

```text
new_dp[(r * num) % k] += dp[r]
```

### 3. Add everything to the answer

Every subarray ending at the current position is a valid operation.

---

## 🔑 Formula

```text
new_remainder = (old_remainder * num) % k
```

---

## 🐍 Python Code

```python
class Solution:
    def resultArray(self, nums, k):
        result = [0] * k
        dp = [0] * k

        for num in nums:
            new_dp = [0] * k

            r = num % k
            new_dp[r] += 1

            for old_r in range(k):
                if dp[old_r]:
                    new_r = (old_r * r) % k
                    new_dp[new_r] += dp[old_r]

            dp = new_dp

            for r in range(k):
                result[r] += dp[r]

        return result
```

---

## ⚠️ Important

The LeetCode method name for this problem is:

```python
resultArray
```

So submit:

```python
class Solution:
    def resultArray(self, nums, k):
```

---

## 🔍 Dry Run

```text
nums = [1, 2, 3]
k = 3
```

### num = 1

```text
[1, 0, 0]
```

Answer:

```text
[1, 0, 0]
```

### num = 2

New subarrays:

```text
[2]       → 2 % 3 = 2
[1, 2]    → 2 % 3 = 2
```

So:

```text
dp = [0, 2, 0]
```

Answer:

```text
[1, 2, 0]
```

### num = 3

New subarrays:

```text
[3]       → 0
[2,3]     → 0
[1,2,3]   → 0
```

So:

```text
dp = [3, 0, 0]
```

Final:

```text
[4, 2, 0]
```

---

## ⏱️ Complexity

Let:

```text
n = len(nums)
```

Since `k <= 5`:

### Time

```text
O(n × k)
```

### Space

```text
O(k)
```

Very efficient because `k` is at most `5`.

---

## 🧠 Easy Memory Trick

Remember the whole solution as:

```text
START → num % k

EXTEND → (old remainder × num) % k

COUNT → add dp to answer
```

### One-line logic

```text
Every subarray = start new + extend old subarrays
```

---

## 📌 Key Concepts

* Dynamic Programming
* Subarrays
* Modular Arithmetic
* Remainders
* Counting
* State Transition

---

## 🔗 LeetCode

Problem:

**3524. Find X Value of Array I**

Platform: LeetCode

Difficulty: Medium
