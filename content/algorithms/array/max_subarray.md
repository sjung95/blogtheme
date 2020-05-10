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

1. Iterate thru the array from the second element. Add the element before to current element iff the element before is greater than zero.
2. Return the max value of the array. 

## Complexity Analysis

### Time: O(N)

We iterate through the array once.

### Space: O(1)

We update the nums array in place.

## Python solution

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        for i in range(1, len(nums)):
            if nums[i-1] > 0:
                nums[i] += nums[i-1]

        return max(nums)
```

## Go solution

```go

func maxSubArray(nums []int) int {
    curr_max := nums[0]
    for i := 1; i < len(nums); i++ {
        if nums[i-1] > 0 {
            nums[i] += nums[i-1]
        }
        if nums[i] > curr_max {
            curr_max = nums[i]
        }
    }
    return curr_max
}
```

## Rust solution

```rust
use std::cmp::{max};

impl Solution {
    pub fn max_sub_array(nums: Vec<i32>) -> i32 {
        let mut nums_clone = nums.clone();
        for i in 1..nums.len() {
            if nums_clone[i-1] > 0 {
                nums_clone[i] += nums_clone[i-1]
            }
        }
        let max_value = nums_clone.iter().max();
        match max_value {
            None => return 0,
            Some(i) => return *i
        }
    }
}

```
