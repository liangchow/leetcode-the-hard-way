---
description: 'Author: @DongDong | https://leetcode.com/problems/score-of-a-string/'
tags: [Two Pointers]
---

# 3110 - Score of a String (Easy)

## Problem Link

https://leetcode.com/problems/score-of-a-string/

## Problem Statement

You are given a string `s`. The **score** of a string is defined as the sum of the absolute difference between the **ASCII** values of adjacent characters.

Return the **score** of `s`.


**Example 1:**

```
Input: s = "hello"
Output: 13
Explanation: The ASCII values of the characters in s are: 'h' = 104, 'e' = 101, 'l' = 108, 'o' = 111. So, the score of s would be |104 - 101| + |101 - 108| + |108 - 108| + |108 - 111| = 3 + 7 + 0 + 3 = 13.
```

**Example 2:**

```
Input: s = "zaz"
Output: 50
Explanation: The ASCII values of the characters in s are: 'z' = 122, 'a' = 97. So, the score of s would be |122 - 97| + |97 - 122| = 25 + 25 = 50.
```

**Constraints:**

- `2 <= s.length <= 100`
- `s` consists only of lowercase English letters.

## Approach 1: Two Pointers

Use a two-pointer approach: the first pointer starts at the beginning of the string `s`, and the second pointer starts at index 1. Iterate through the string, and at each step, add the absolute difference between the ASCII values (converted using `ord()`) of the two characters to `res`.

Time Complexity: $O(n)$

Space Complexity: $O(1)$

<Tabs>
<TabItem value="python" label="Python">
<SolutionAuthor name="@DongDong"/>

```py
class Solution:
    def scoreOfString(self, s: str) -> int:
        i = 0
        res = 0
        for j in range(1, len(s)):
            res += abs(ord(s[i]) - ord(s[j]))
            i += 1
        return res
```

</TabItem>
</Tabs>
