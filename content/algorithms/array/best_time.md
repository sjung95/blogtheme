+++
title = "Best Time to Buy and Sell Stock"
date = 2020-05-09
description = "Array"
insert_anchor_links = "right"

[taxonomies]
tags = ["Array"]
authors = ["Suzie Jung"]
+++

## How to solve

1. Initialize min price to infinity and max profit to zero.
2. Iterate through the price array and update min_price, then update max_profit.
3. Return max_profit.

## Complexity Analysis

### Time: O(N)

We iterate through the price array once.

### Space: O(1)

We only use two constant variables.

## Python solution

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        min_price = float('inf')
        max_profit = 0

        for p in prices:
            min_price = min(min_price, p)
            profit = p - min_price
            max_profit = max(max_profit, profit)

        return max_profit
```

## Go solution

```go
func maxProfit(prices []int) int {
    min_price := math.MaxInt32
    max_profit := 0

    for _, price := range prices {
        if price < min_price {
            min_price = price
        }
        profit := price - min_price
        if max_profit < profit {
            max_profit = profit
        }
    }
    return max_profit
}
```

## Rust solution

```rust
use std::cmp::{min, max};

impl Solution {
    pub fn max_profit(prices: Vec<i32>) -> i32 {
        let mut min_price = std::i32::MAX;
        let mut max_profit = 0;

        for &price in &prices {
            min_price = min(price, min_price);
            let profit = price - min_price;
            max_profit = max(profit, max_profit);
        }
        max_profit
    }
}
```
