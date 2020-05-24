+++
title = "House Robber II"
date = 2020-05-21
description = "Dynamic Programming"
insert_anchor_links = "right"

[taxonomies]
tags = ["Dynamic Programming"]
authors = ["Suzie Jung"]
+++

## How to solve

1. First, check for a simple case. If the number of houses is less than 4, The maximum profit that can be made is the maximum of the money stashed at each house. This is because if there are less than 4 houses, a robber can only rob one house due to the circular arrangement nature.
2. Otherwise, we solve the problem by splitting the problem in to two steps.
    * First step: iterate through from the house at index 1 to the last house (inclusive). Note that this is to avoid the case of robbing the last house and house at index 0 (which are adjacent houses since the houses are in circular arrangement).
    * Second step: iterate through from house at index 9 to the second to last house (inclusive).
3. While iterating through each step, we keep track of the maximum profit made one house ago and the maximum profit made two houses ago.
    * The max profit made one house ago may or may not include that house one house ago, and the max profit made two houses ago may or may not include that house two houses ago.
    * At a given house, update the max profit made "two houses ago" and max profit made "one house ago" (these updates have to happen in one line in the cases of python and go; rust requires temp variables).
        * Max profit made two houses ago gets updated to the max profit made one house ago.
        * Max profit made one house ago gets updated (this is now including the given house) by taking the max of (profit made two houses ago + amount at a given house) and (profit made one house ago). Update the max profit made "two houses ago."
4. Return the max of the final results at each step.

## Complexity Analysis

### Time: O(N)

We iterate through the n-1 elements of the nums array twice. So O(2*(n-1)) = O(n).

### Space: O(1)

We use constant space by storing intermediate results in variables.

## Python solution

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        if not nums:
            return 0
        if len(nums) < 4:
            return max(nums)

        two_houses_ago = 0
        one_house_ago = 0

        for i in range(1, len(nums)):
            two_houses_ago, one_house_ago = one_house_ago, max(two_houses_ago + nums[i], one_house_ago)

        result = one_house_ago

        two_houses_ago = 0
        one_house_ago = 0

        for i in range(len(nums) - 1):
            two_houses_ago, one_house_ago = one_house_ago, max(two_houses_ago + nums[i], one_house_ago)

        return max(result, one_house_ago)
```

## Go solution

```go
func rob(nums []int) int {
    switch nums_len := len(nums); nums_len {
        case 0:
        return 0
        case 1:
        return nums[0]
        case 2:
        return max(nums[0], nums[1])
        case 3:
        return max(nums[0], max(nums[1], nums[2]))
    }

    two_houses_ago := 0
    one_house_ago := 0

    for i := 1; i < len(nums); i++ {
        two_houses_ago, one_house_ago = one_house_ago, max(two_houses_ago + nums[i], one_house_ago)
    }

    result := one_house_ago
    two_houses_ago = 0
    one_house_ago = 0

    for i := 0; i < len(nums) - 1; i++ {
        two_houses_ago, one_house_ago = one_house_ago, max(two_houses_ago + nums[i], one_house_ago)
    }
    return max(result, one_house_ago)
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
            return 0
        }s
        match nums.len() {
            1 => return nums[0],
            2 => return max(nums[0], nums[1]),
            3 => return max(nums[0], max(nums[1], nums[2])),
            _ => {
                let mut two_houses_ago = 0;
                let mut one_house_ago = 0;

                for i in 1..nums.len() {
                    let mut prev_two = two_houses_ago;
                    let mut prev_one = one_house_ago;
                    two_houses_ago = one_house_ago;
                    one_house_ago = max(prev_two + nums[i], prev_one)
                }

                let mut result = one_house_ago;

                two_houses_ago = 0;
                one_house_ago = 0;

                for i in 0..nums.len() - 1 {
                    let mut prev_two = two_houses_ago;
                    let mut prev_one = one_house_ago;
                    two_houses_ago = one_house_ago;
                    one_house_ago = max(prev_two + nums[i], prev_one)
                }

                return max(one_house_ago, result)
            }
        }
    }
}
```
