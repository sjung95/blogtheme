+++
title = "Maximum Product Subarray"
date = 2020-05-11
description = "Array"
insert_anchor_links = "right"

[taxonomies]
tags = ["Array"]
authors = ["Suzie Jung"]
+++

## How to solve

1. Set prev_min, prev_max, and ans to the first number in the nums array.
2. Iterate through the array from the second element. Set curr_max/curr_min as the max/min of prev_max*num, prev_min*num, and num.
3. Update ans as the max of curr_max and curr_min.
4. Set prev_max/prev_min to curr_max/curr_min.
5. Return the answer.

## Complexity Analysis

### Time: O(N)

We iterate through the array once.

### Space: O(1)

We only use variables.

## Python solution

```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        prev_max = nums[0]
        prev_min = nums[0]
        ans = nums[0]

        for i in range(1, len(nums)):
            curr_max = max(prev_max*nums[i], prev_min*nums[i], nums[i])
            curr_min = min(prev_max*nums[i], prev_min*nums[i], nums[i])
            ans = max(curr_max, ans)

            prev_max = curr_max
            prev_min = curr_min

        return ans
```

## Go solution

```go
func maxProduct(nums []int) int {
    prev_max := nums[0]
    prev_min := nums[0]
    ans := nums[0]

    for i := 1; i < len(nums); i++ {
        curr_max := max(max(prev_max*nums[i], prev_min*nums[i]), nums[i])
        curr_min := min(min(prev_max*nums[i], prev_min*nums[i]), nums[i])
        ans = max(curr_max, ans)
        prev_max = curr_max
        prev_min = curr_min
    }
    return ans
}

func max(a, b int) int {
        if a > b {
            return a
        }
        return b
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
use std::cmp::{min, max};

impl Solution {
    pub fn max_product(nums: Vec<i32>) -> i32 {
        let mut prev_max = nums[0];
        let mut prev_min = nums[0];
        let mut ans = nums[0];

        for i in 1..nums.len() {
            let mut curr_max = max(max(prev_max*nums[i], prev_min*nums[i]), nums[i]);
            let mut curr_min = min(min(prev_max*nums[i], prev_min*nums[i]), nums[i]);
            ans = max(curr_max, ans);
            prev_max = curr_max;
            prev_min = curr_min
        }

        ans
    }
}
```
