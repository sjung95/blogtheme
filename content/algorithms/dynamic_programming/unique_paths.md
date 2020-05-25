+++
title = "Unique Paths"
date = 2020-05-25
description = "Dynamic Programming"
insert_anchor_links = "right"

[taxonomies]
tags = ["Dynamic Programming"]
authors = ["Suzie Jung"]
+++

## How to solve

1. Initialize a 2d dp array that will represent the board. Each entry is the number of ways to get to that cell.
2. The first row and the first col are set to zero. This is because there is one way to get to each cell in the first row and the first col.
3. With this base case set up, build out the rest of the array. The number of ways to get to a cell (i, j) is the number of ways to get to (i-1, j) + number of ways to get to (i, j-1).
4. Return the number in the bottom right corner cell.

## Complexity Analysis

### Time: O(m*n)

We iterate through the matrix once.

### Space: O(m*n)

We utilize a 2d dp array that has size m*n.

## Python solution

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [[0 for _ in range(n)] for _ in range(m)]

        for i in range(m):
            dp[i][0] = 1
        for i in range(n):
            dp[0][i] = 1

        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i-1][j] + dp[i][j-1]

        return dp[-1][-1]
```

## Go solution

```go
func uniquePaths(m int, n int) int {
    dp := make([][]int, m)
    for i := 0; i < m; i++ {
        dp[i] = make([]int, n)
    }

    for i := 0; i < m; i++ {
        dp[i][0] = 1
    }

    for i := 0; i < n; i++ {
        dp[0][i] = 1
    }

    for i := 1; i < m; i++ {
        for j := 1; j < n; j++ {
            dp[i][j] = dp[i-1][j] + dp[i][j-1]
        }
    }

    return dp[m-1][n-1]
}
```

## Rust solution

```rust
impl Solution {
    pub fn unique_paths(m: i32, n: i32) -> i32 {
        let mut rows = vec![0; n as usize];
        let mut dp = vec![rows; m as usize];
        let m = m as usize;
        let n = n as usize;
        for i in 0..m {
            dp[i][0] = 1
        }

        for i in 0..n {
            dp[0][i] = 1
        }

        for i in 1..m {
            for j in 1..n {
                dp[i][j] = dp[i-1][j] + dp[i][j-1]
            }
        }

        dp[m-1][n-1]
    }
}
```
