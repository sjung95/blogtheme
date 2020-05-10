+++
title = "Maximum Subarray"
date = 2020-05-10
description = "Array"
insert_anchor_links = "right"

[taxonomies]
tags = ["Array"]
authors = ["Suzie Jung"]
+++

## How to solve

1. Set the current sum and the max sum to the first element of the array.
2. Iterate through the array from the second element. Update the current sum and the max sum.
3. Return the max sum.

## Complexity Analysis

### Time: O(N)

We iterate through the array once.

### Space: O(1)

We update the nums array in place.

## Python solution

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        if not nums:
            return 0

        curr_sum = nums[0]
        max_sum = nums[0]
        for i in range(1, len(nums)):
            curr_sum = max(nums[i], curr_sum + nums[i])
            max_sum = max(curr_sum, max_sum)

        return max_sum

```

## Go solution

```go

func maxSubArray(nums []int) int {
    if len(nums) == 0 {
        return 0
    }

    curr_sum := nums[0]
    max_sum := nums[0]

    for i := 1; i < len(nums); i++ {
        if nums[i] > curr_sum + nums[i] {
            curr_sum = nums[i]
        } else {
            curr_sum += nums[i]
        }

        if curr_sum > max_sum {
            max_sum = curr_sum
        }
    }
    return max_sum
}
```

## Rust solution

```rust
use std::cmp::{max};

impl Solution {
    pub fn max_sub_array(nums: Vec<i32>) -> i32 {
        if nums.len() == 0 {
            return 0
        }
        let mut curr_sum = nums[0];
        let mut max_sum = nums[0];

        for i in 1..nums.len() {
            curr_sum = max(nums[i], curr_sum + nums[i]);
            max_sum = max(max_sum, curr_sum)
        }
        max_sum
    }
}

```
