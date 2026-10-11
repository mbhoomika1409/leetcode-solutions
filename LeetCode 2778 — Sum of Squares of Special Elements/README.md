# LeetCode 2778 — Sum of Squares of Special Elements

**Difficulty:** Easy

## Problem

Given a 1-indexed integer array `nums` of length `n`, an element `nums[i]` is called special if its index `i` divides `n` evenly.

Return the sum of the squares of all special elements.

## Logic

1. Find the length of the array using `n = len(nums)`.
2. Initialize `total = 0` to store the answer.
3. Traverse the array using a loop.
4. Python uses 0-based indexing, so use `i + 1` to get the 1-based index.
5. Check whether `n % (i + 1) == 0`.
6. If the condition is true, add the square of `nums[i]` to `total`.
7. Return `total`.

## Python Code

```python
class Solution:
    def sumOfSquares(self, nums: list[int]) -> int:
        n = len(nums)
        total = 0

        for i in range(n):
            if n % (i + 1) == 0:
                total += nums[i] ** 2

        return total
```

## Example 1

**Input:**
```text
nums = [1, 2, 3, 4]
```

Array length: `n = 4`

| Index (1-based) | Value | Special? | Square |
|---:|---:|---|---:|
| 1 | 1 | Yes | 1 |
| 2 | 2 | Yes | 4 |
| 3 | 3 | No | 0 |
| 4 | 4 | Yes | 16 |

**Calculation:**

```text
1² + 2² + 4² = 1 + 4 + 16 = 21
```

**Output:**
```text
21
```

## Example 2

**Input:**
```text
nums = [2, 7, 1, 19, 18, 3]
```

Array length: `n = 6`

The special indices are `1, 2, 3, 6`.

**Calculation:**

```text
2² + 7² + 1² + 3²
= 4 + 49 + 1 + 9
= 63
```

**Output:**
```text
63
```

## Important Code Explanation

- `n = len(nums)` — finds the array length.
- `total = 0` — initializes the sum.
- `range(n)` — visits every array position.
- `i + 1` — converts Python's 0-based index to the problem's 1-based index.
- `n % (i + 1) == 0` — checks whether the index divides the array length evenly.
- `nums[i] ** 2` — calculates the square of the current element.
- `total += nums[i] ** 2` — adds the square to the sum.
- `return total` — returns the final answer.

## Complexity Analysis

- **Time Complexity:** `O(n)` — each element is checked once.
- **Space Complexity:** `O(1)` — only a constant amount of extra space is used.

## Key Takeaway

The main condition is:

```python
if n % (i + 1) == 0:
```

If the 1-based index divides the array length evenly, square that element and add it to the total.
