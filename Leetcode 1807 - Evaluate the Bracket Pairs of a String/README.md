━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FILE: solution.py
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

class Solution:
    def evaluate(self, s, knowledge):
        data = dict(knowledge)

        result = []
        i = 0

        while i < len(s):
            if s[i] == '(':
                i += 1
                key = ""

                while s[i] != ')':
                    key += s[i]
                    i += 1

                result.append(data.get(key, '?'))
            else:
                result.append(s[i])

            i += 1

        return ''.join(result)


━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FILE: README.md
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

# Evaluate the Bracket Pairs of a String

## Problem

Given a string `s` containing bracket pairs and a list of key-value pairs called `knowledge`, replace every bracket pair with its corresponding value.

If a key is not present in `knowledge`, replace the bracket pair with `?`.

## Example

### Input

s = "(name)is(age)yearsold"
knowledge = [["name","bob"],["age","two"]]

### Output

"bobistwoyearsold"

## Approach

1. Convert `knowledge` into a dictionary.
2. Traverse the string character by character.
3. When `(` is found, collect the key until `)`.
4. Check whether the key exists in the dictionary.
5. If the key exists, add its value to the result.
6. If the key does not exist, add `?`.
7. Add normal characters directly to the result.
8. Join the result to get the final string.

## Examples

### Example 1

Input:
s = "(name)is(age)yearsold"
knowledge = [["name","bob"],["age","two"]]

Output:
"bobistwoyearsold"

### Example 2

Input:
s = "hi(name)"
knowledge = [["a","b"]]

Output:
"hi?"

### Example 3

Input:
s = "(a)(a)(a)aaa"
knowledge = [["a","yes"]]

Output:
"yesyesyesaaa"

## Key Concept

- Dictionary / Hash Map
- String Traversal
- String Parsing

## Complexity

Time Complexity: O(n + k)

Space Complexity: O(k)

Where:
- n = length of the string
- k = number of knowledge pairs

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
GITHUB COMMANDS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

git add .

git commit -m "Solve Evaluate the Bracket Pairs of a String"

git push

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
COMMIT MESSAGE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Solve Evaluate the Bracket Pairs of a String
