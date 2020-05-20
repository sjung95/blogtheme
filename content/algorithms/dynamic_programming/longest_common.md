+++
title = "Longest Common Subsequence"
date = 2020-05-19
description = "Dynamic Programming"
insert_anchor_links = "right"

[taxonomies]
tags = ["Dynamic Programming"]
authors = ["Suzie Jung"]
+++

## How to solve

1. The main idea is to use a 2d array with rows being the alphabets in text1 and cols being the alphabets in text2.
2. We iterate through the 2d array and populate it. Denoting m=len(text1) and n=len(text2), the 2d array will have size (m+1) * (n+1). We need the extra entries before the first letters as we will be building this array bottom-up and need the base case.
    * Initialize the 2d array to zeroes.
    * In a nested for loop, we iterate through the row and the col. For each alphabet at index i of text 1 and index j of text2, check if they're equal.
        * If equal, the current longest common subsequence is the length of the longest common subsequence at row i-1 and col j - 1 plus 1.
        * If not, the current longest common subsequence is the maximum of the value at row i-1 and col j or the value at row i and col j-1.
3. The last entry in the 2d array (bottom-most, rightmost) is the answer.

## Complexity Analysis

### Time: O(m*n)

Assuming len(text1) == m and len(text2) == n, for each letter in m we iterate through n times.

### Space: O(m*n)

The 2d array takes (m+1) \* (n+1) ~= m*n space

## Python solution

```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        m = len(text1)
        n = len(text2)

        dp = [[0 for _ in range(n+1)] for _ in range(m+1)]

        for i in range(m):
            for j in range(n):
                if text1[i] == text2[j]:
                    dp[i+1][j+1] = dp[i][j] + 1
                else:
                    dp[i+1][j+1] = max(dp[i+1][j], dp[i][j+1])

        return dp[-1][-1]
```

## Go solution

```go
func longestCommonSubsequence(text1 string, text2 string) int {
    m := len(text1)
    n := len(text2)

    dp := make([][]int, m+1)
    for i := 0; i < m+1; i++ {
        dp[i] = make([]int, n+1)
    }

    for i := 0; i < m; i++ {
        for j := 0; j < n; j++ {
            if text1[i] == text2[j] {
                dp[i+1][j+1] = dp[i][j] + 1
            } else {
                dp[i+1][j+1] =  max(dp[i+1][j], dp[i][j+1])
            }
        }
    }

    return dp[m][n]
}

func max(a int, b int) int {
    if a > b {
        return a
    }
    return b
}
```

## Rust solution

```rust
use std::cmp::max;

impl Solution {
    pub fn longest_common_subsequence(text1: String, text2: String) -> i32 {
        let m = text1.len();
        let n = text2.len();

        let mut rows = vec![0; n+1];
        let mut dp = vec![rows; m+1];

        for (i, c1) in text1.chars().enumerate() {
            for (j, c2) in text2.chars().enumerate() {
                if c1 == c2 {
                    dp[i+1][j+1] = dp[i][j] + 1;
                }
                else {
                    dp[i+1][j+1] = max(dp[i+1][j], dp[i][j+1]);
                }
            }
        }
        dp[m][n]
    }
}
```
