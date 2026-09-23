## Problem

You are given an integer array `nums` and an integer `x`.

In one operation, you can remove either:

* The leftmost element
* The rightmost element

The removed element is subtracted from `x`.

The goal is to reduce `x` to **exactly `0`** using the **minimum number of operations**.

If it is not possible, return `-1`.

---

## Example 1

### Input

```text
nums = [1,1,4,2,3]
x = 5
```

### Explanation

Remove `3` from the right:

```text
x = 5 - 3 = 2
```

Then remove `2` from the right:

```text
x = 2 - 2 = 0
```

So the answer is:

```text
2
```

---

## Example 2

### Input

```text
nums = [5,6,7,8,9]
x = 4
```

It is impossible to subtract elements from the ends and get exactly `4`.

### Output

```text
-1
```

---

## Example 3

### Input

```text
nums = [3,2,20,1,1,3]
x = 10
```

Total sum:

```text
3 + 2 + 20 + 1 + 1 + 3 = 30
```

We need to remove elements whose sum is `10`.

Instead of finding the elements to remove, we can find the elements to keep.

Required remaining sum:

```text
30 - 10 = 20
```

The longest subarray with sum `20` is:

```text
[20]
```

Its length is `1`.

Array length is `6`.

Therefore:

```text
minimum operations = 6 - 1 = 5
```

### Output

```text
5
```

---

# Approach

The main idea is to convert the problem into a **longest subarray problem**.

Let:

```text
total = sum(nums)
```

If we remove elements with sum `x`, the remaining elements must have:

```text
remaining_sum = total - x
```

Since we can only remove elements from the left or right, the elements that remain must form a **continuous subarray**.

Therefore, we need to:

1. Calculate the total sum.
2. Calculate the target:

   ```text
   target = total - x
   ```
3. Find the **longest continuous subarray** whose sum is `target`.
4. The elements outside this subarray are the elements we remove.
5. Therefore:

   ```text
   minimum operations = n - longest_subarray_length
   ```

---

# Why Sliding Window?

All values in `nums` are positive.

Because of this, we can use the **sliding window / two-pointer technique**.

We maintain:

```text
left
right
current_sum
```

For every `right`:

* Add `nums[right]` to `current_sum`.
* If `current_sum > target`, move `left` forward.
* If `current_sum == target`, calculate the length of the current window.
* Keep the maximum window length.

---

# Algorithm

```text
1. Calculate total = sum(nums)

2. Calculate target = total - x

3. If target < 0:
       return -1

4. Use two pointers:
       left = 0
       current_sum = 0
       max_len = -1

5. Move right from 0 to n-1:
       Add nums[right] to current_sum

6. While current_sum > target:
       Subtract nums[left]
       Move left forward

7. If current_sum == target:
       Update max_len

8. If no valid subarray exists:
       return -1

9. Otherwise:
       return n - max_len
```

---

# Python Solution

```python
class Solution:
    def minOperations(self, nums, x):
        target = sum(nums) - x

        if target < 0:
            return -1

        left = 0
        current_sum = 0
        max_len = -1

        for right in range(len(nums)):
            current_sum += nums[right]

            while current_sum > target and left <= right:
                current_sum -= nums[left]
                left += 1

            if current_sum == target:
                max_len = max(max_len, right - left + 1)

        if max_len == -1:
            return -1

        return len(nums) - max_len
```

---

# Dry Run

For:

```text
nums = [1,1,4,2,3]
x = 5
```

### Step 1 — Total sum

```text
total = 11
```

### Step 2 — Target

```text
target = 11 - 5
       = 6
```

Now we need the longest subarray with sum `6`.

We find:

```text
[1,1,4]
```

Sum:

```text
1 + 1 + 4 = 6
```

Length:

```text
3
```

Array length:

```text
5
```

Therefore:

```text
answer = 5 - 3
       = 2
```

---

# Complexity

### Time Complexity

```text
O(n)
```

Each element is added to the sliding window once and removed at most once.

### Space Complexity

```text
O(1)
```

Only a few variables are used.

---

# Important Concept

The key transformation is:

```text
Remove elements with sum X
          ↓
Keep elements with sum total - X
          ↓
Find the longest continuous subarray
          ↓
Minimum operations = n - longest length
```

---

# Pattern to Remember

This problem is an important **Sliding Window + Prefix Sum idea**.

When you see:

> Remove elements from both ends and minimize the number of removals

Think:

```text
What can I KEEP?
```

Then convert it into:

```text
Find the longest subarray with the required sum.
```

---

## Constraints

```text
1 <= nums.length <= 10^5
1 <= nums[i] <= 10^4
1 <= x <= 10^9
```

Because `nums[i]` are positive, the sliding window approach works efficiently.

---

## Topics

* Array
* Sliding Window
* Two Pointers
* Prefix Sum
* Hash Table
* Binary Search

---

## LeetCode

**Problem:** 1658. Minimum Operations to Reduce X to Zero

**Difficulty:** Medium

**Main Technique:** Sliding Window / Two Pointers

**Language:** Python
