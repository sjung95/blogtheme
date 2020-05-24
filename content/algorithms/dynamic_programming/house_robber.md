+++
title = "House Robber"
date = 2020-05-21
description = "Dynamic Programming"
insert_anchor_links = "right"

[taxonomies]
tags = ["Dynamic Programming"]
authors = ["Suzie Jung"]
+++

## How to solve

1. First, check for edge cases. If len(nums)==0, just return 0. If len(nums)==1, just return the only element in the nums array.
2. Initialize a dp array. This array will keep track of maximum profit that can be made up to and including/not including the house at index i.
3. Establish the base case.
    * The max profit that can be made robbing up to the house at index 0 is nums[0].
    * The max profit that can be made robbing up to the house at index 1 is the max of nums[0] and nums[1] (robber either robs house 0 or house 1).
4. Iterate through the rest of the nums array and populate the dp array by setting the dp at index i to the max of (profit of robbing up to and including house at i-2 + profit of robbing house i) and (profit of robbing up to and including house at i-1).
5. Return the last element of the dp array.

## Complexity Analysis

### Time: O(N)

We iterate through the nums array once, which takes linear time.

### Space: O(N)

We use a dp array that has length N. 

## Python solution

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        if len(nums) == 0:
            return 0
        elif len(nums) == 1:
            return nums[0]

        dp = [0 for _ in range(len(nums))]
        dp[0] = nums[0]
        dp[1] = max(nums[0], nums[1])

        for i in range(2, len(nums)):
            dp[i] = max(dp[i-1], dp[i-2] + nums[i])

        return dp[-1]
```

## Go solution

```go
func rob(nums []int) int {
    if len(nums) == 0 {
        return 0
    }
    if len(nums) == 1 {
        return nums[0]
    }

    dp := make([] int, len(nums))
    dp[0] = nums[0]
    dp[1] = max(nums[0], nums[1])

    for i := 2; i < len(nums); i++ {
        dp[i] = max(dp[i-2] + nums[i], dp[i-1])
    }

    return dp[len(nums) - 1]
}

func max(a, b int) int {
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
    pub fn rob(nums: Vec<i32>) -> i32 {
        if nums.len() == 0 {
            return 0;
        }
        if nums.len() == 1 {
            return nums[0];
        }

        let mut dp = vec![0; nums.len()];
        dp[0] = nums[0];
        dp[1] = max(nums[0], nums[1]);

        for i in 2..nums.len() {
            dp[i] = max(dp[i-2] + nums[i], dp[i-1])
        }

        dp[nums.len() - 1]
    }
}
```
