+++
title = "Decode Ways"
date = 2020-05-23
description = "Dynamic Programming"
insert_anchor_links = "right"

[taxonomies]
tags = ["Dynamic Programming"]
authors = ["Suzie Jung"]
+++

## How to solve

1. Check the base cases first. If the string is empty or if the first letter in the string is a '0', return 0.
2. Initialize a dp array of zeroes with length as the length of string. This dp array will contain how many ways to decode up to and including the index.
3. Set the first element in the dp array to 1, since there is 1 way to decode one character (we don't have to worry that the first character will be '0' since we checked for it in step 1).
4. Iterate through the string from index 1 until the end.
    * If the current character is not 0, this means this character can be decoded on its own. Thus, add the ways to decode up to and including the char at i-1 (dp[i-1]) and add it to dp[i].
    * If the character before and the current character make up a number in [10, 26].
        * If i == 1 (this is the special one-off case to check to prevent out-of-bounds index error), add 1 to the number of ways to decode to dp[1].
        * Ohterwise, add dp[i-2] ways to dp[i].
5. Return the last element in the dp array.

## Complexity Analysis

### Time: O(N)

We iterate through all the characters of string s.

### Space: O(N)

We utilize a dp array that has size of length of string s.

## Python solution

```python
class Solution:
    def numDecodings(self, s: str) -> int:
        if not s:
            return 0

        if s[0] == '0':
            return 0

        dp = [0 for _ in range(len(s))]

        dp[0] = 1

        for i in range(1, len(s)):
            if s[i] != '0':
                dp[i] += dp[i-1]
            if 10 <= int(s[i-1:i+1]) <= 26:
                if i == 1:
                    dp[i] += 1
                else:
                    dp[i] += dp[i-2]

        return dp[-1]
```

## Go solution

```go
func numDecodings(s string) int {
    if len(s) == 0 {
        return 0
    }

    if s[0] == '0' {
        return 0
    }

    dp := make([] int, len(s))
    dp[0] = 1

    for i := 1; i < len(s); i++ {
        if s[i] != '0' {
            dp[i] += dp[i-1]
        }
        num := int(s[i-1] - '0') * 10 + int(s[i] - '0')
        if num >= 10 && num <= 26 {
            if i == 1 {
                dp[i] += 1
            } else {
                dp[i] += dp[i-2]
            }
        }
    }
    return dp[len(s) - 1]
}
```

## Rust solution

```rust
impl Solution {
    pub fn num_decodings(s: String) -> i32 {
        if s.len() == 0 {
            return 0;
        }

        let char_array = s.as_bytes();

        if char_array[0] == b'0' {
            return 0;
        }

        let mut dp = vec![0; s.len()];
        dp[0] = 1;

        for i in 1..s.len() {
            if char_array[i] != b'0' {
                dp[i] += dp[i-1];
            }
            let mut num = (char_array[i-1] - b'0') * 10 + (char_array[i] - b'0');
            if num >=10 && num <= 26 {
                if i == 1 {
                    dp[i] += 1;
                }
                else {
                    dp[i] += dp[i-2];
                }
            }
        }
        dp[s.len() - 1]
    }
}
```
