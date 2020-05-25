+++
title = "Coin Change"
date = 2020-05-18
description = "Dynamic Programming"
insert_anchor_links = "right"

[taxonomies]
tags = ["Dynamic Programming"]
authors = ["Suzie Jung"]
+++

## How to solve

1. Initialize the dp array: this array will store the min number of coins to make the index amount.
    * Note the dp array will be of length amount + 1.
    * Initially, the first element will be set to 0 since there are 0 ways to make 0. Other entries are set to max possible number.
2. For each coin in coins, update the dp array by iterating from idx = coin to idx = amount.
    * If dp[curr_amount-coin] + 1 is less than dp[curr_amount], update it.
3. After all iteration, if the last element in the dp array is still max number, there is no way to make this amount with the given coins. Thus return -1. Otherwise return the last element.

## Complexity Analysis

### Time: O(N*c)

N denotes amount.
For each coin, the algorithm iterates from coin value to amount (worst case N iterations).

### Space: O(N)

The ways to make N is stored for each amount from 0 to N.

## Python solution

```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [(amount+1) for _ in range(amount + 1)]

        dp[0] = 0

        for coin in coins:
            for i in range(coin, amount+1):
                dp[i] = min(dp[i-coin] + 1, dp[i])

        if dp[-1] == amount+1:
            return -1

        return dp[-1]
```

## Go solution

```go
func coinChange(coins []int, amount int) int {
    dp := make([]int, amount+1)

    for i := 0; i < amount + 1; i++ {
        dp[i] = amount + 1
    }

    dp[0] = 0

    for _, coin := range coins {
        for i := coin; i < amount + 1; i ++ {
            dp[i] = min(dp[i], dp[i-coin] + 1)

        }
    }

    if dp[amount] == amount+1 {
        return -1
    }

    return dp[amount]
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}
```

## Rust solution

```rust
use std::cmp::min;

impl Solution {
    pub fn coin_change(coins: Vec<i32>, amount: i32) -> i32 {
        let mut dp = vec![(amount+1); (amount+1) as usize];
        dp[0] = 0;

        for &coin in &coins {
            for i in coin..amount+1 {
                let coin = coin as usize;
                let i = i as usize;
                dp[i] = min(dp[i], dp[(i-coin)] + 1)
            }
        }

        if dp[amount as usize] == amount + 1 {
            return -1
        }
        return dp[amount as usize]
    }
}
```
