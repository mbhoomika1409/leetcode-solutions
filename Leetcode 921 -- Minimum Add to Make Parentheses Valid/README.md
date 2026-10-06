Minimum Add to Make Parentheses Valid

==================================================
1. PROBLEM STATEMENT
==================================================

A parentheses string is valid if and only if:

- It is the empty string.
- It can be written as AB, where both A and B are valid strings.
- It can be written as (A), where A is a valid string.

You are given a parentheses string s.

In one move, you can insert either ( or ) at any position in the string.

Return the minimum number of moves required to make s valid.


Example 1:

Input: s = "())"
Output: 1


Example 2:

Input: s = "((("
Output: 3


==================================================
2. UNDERSTANDING THE QUESTION
==================================================

The main thing we need to understand is that every opening
parenthesis ( needs a matching closing parenthesis ).

For example:

()

is valid because the ( has a matching ).

This is also valid:

(())

But this is invalid:

())

because there is one extra ).

And this is invalid:

(((

because there are three unmatched (.

So our goal is to find how many parentheses we need to insert.


==================================================
3. HOW TO THINK ABOUT THE PROBLEM
==================================================

Instead of immediately thinking about code, first decide
what information we need to remember.

We need to keep track of:

open = number of unmatched '('
answer = number of insertions required

We scan the string from left to right.


==================================================
4. WHAT HAPPENS WHEN WE SEE '('?
==================================================

Suppose we see:

(

This means we have one more opening parenthesis available.

So:

open = open + 1

Example:

(((
 
After reading each character:

(    -> open = 1
((   -> open = 2
(((  -> open = 3


==================================================
5. WHAT HAPPENS WHEN WE SEE ')'?
==================================================

A closing parenthesis ) needs an opening parenthesis (
to match it.

There are two cases.


CASE 1: WE HAVE AN UNMATCHED '('

If:

open > 0

then we can match the current ) with one (.

So:

open = open - 1

Example:

()

First:

( -> open = 1

Then:

) -> open = 0

The pair is matched.


CASE 2: WE DO NOT HAVE AN UNMATCHED '('

If:

open == 0

and we see:

)

there is no ( available to match it.

So we must insert an opening parenthesis (.

Therefore:

answer = answer + 1

Example:

())

After processing:

( -> open = 1
) -> open = 0
) -> no '(' available

So we need to insert one (.

The answer becomes:

answer = 1


==================================================
6. WHAT HAPPENS AT THE END?
==================================================

After processing the complete string, we may still have
unmatched opening parentheses.

For example:

(((

At the end:

open = 3

These three ( need three ).

So:

answer = answer + open

Therefore:

answer = 3


==================================================
7. BUILDING THE CODE STEP BY STEP
==================================================

First, create the two variables:

open = 0
answer = 0

Then we need to check every character in the string:

for ch in s:

Now check whether the character is (:

if ch == '(':
    open += 1

Otherwise, the character is ).

We check whether we have an opening parenthesis available:

if open > 0:
    open -= 1

If we don't have one:

else:
    answer += 1

Finally, handle any unmatched ( remaining:

answer += open

Then return the answer:

return answer


==================================================
8. COMPLETE LOGIC
==================================================

The complete logic in simple words:

If we see '(':
    increase open

If we see ')':
    If an '(' is available:
        match it
        decrease open
    Otherwise:
        insert '('
        increase answer

After the string is finished:
    Every remaining '(' needs a ')'
    Add open to answer


==================================================
9. DRY RUN
==================================================

Let's take:

s = "())(()"

Initially:

open = 0
answer = 0


Character 1: '('

open = 1
answer = 0


Character 2: ')'

We have an opening parenthesis available, so match it.

open = 0
answer = 0


Character 3: ')'

There is no opening parenthesis available.

We need to insert '('.

open = 0
answer = 1


Character 4: '('

open = 1
answer = 1


Character 5: '('

open = 2
answer = 1


Character 6: ')'

Match it with one opening parenthesis.

open = 1
answer = 1


The string is finished.

But:

open = 1

There is still one unmatched '('.

So we need one ).

answer = 1 + 1
answer = 2

Final answer:

2


==================================================
10. EXAMPLE 1
==================================================

s = "())"

Processing:

( -> open = 1
) -> open = 0
) -> no opening parenthesis

We need one insertion.

answer = 1

Output:

1


==================================================
11. EXAMPLE 2
==================================================

s = "((("

Processing:

( -> open = 1
( -> open = 2
( -> open = 3

At the end:

open = 3

So we need three ).

answer = 3

Output:

3


==================================================
12. ALGORITHM
==================================================

1. Set open = 0.
2. Set answer = 0.
3. Traverse the string from left to right.
4. If the character is (, increase open.
5. If the character is ):
   - If open > 0, decrease open.
   - Otherwise, increase answer.
6. After processing the complete string, add open to answer.
7. Return answer.


==================================================
13. COMPLEXITY
==================================================

Time Complexity:

O(n)

We visit every character once.


Space Complexity:

O(1)

We only use two variables:

open
answer

No extra data structure is required.


==================================================
14. COMPLETE LEETCODE CLASS SOLUTION
==================================================

class Solution:
    def minAddToMakeValid(self, s):
        open = 0
        answer = 0

        for ch in s:
            if ch == '(':
                open += 1
            else:
                if open > 0:
                    open -= 1
                else:
                    answer += 1

        answer += open

        return answer


==================================================
15. KEY LEARNING
==================================================

The most important part of this problem is understanding
the logic instead of memorizing the code.

Remember:

'(' -> increase open

')' with an available '('
    -> match them
    -> decrease open

')' with no available '('
    -> insert '('
    -> increase answer

remaining '(' at the end
    -> insert ')' for each one


==================================================
16. GENERAL PROBLEM-SOLVING PATTERN
==================================================

Understand the question
        ↓
Identify what needs to be tracked
        ↓
Find the possible cases
        ↓
Decide what happens in each case
        ↓
Write the loop
        ↓
Convert each step into code
        ↓
Dry run with an example
        ↓
Check complexity
