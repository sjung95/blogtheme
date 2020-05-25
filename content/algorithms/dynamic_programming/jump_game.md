+++
title = "Jump Game"
date = 2020-05-25
description = "Dynamic Programming"
insert_anchor_links = "right"

[taxonomies]
tags = ["Dynamic Programming"]
authors = ["Suzie Jung"]
+++

## How to solve

1. We keep track of the current max index, which denotes the max index we can jump to at a given time. This variable will allow us to determine whether we can reach the last index.
2. Initialize the current max index to 0.
3. We iterate through nums.
    * If the index of the number in nums we are considering is greater than our current max index, this means that there is no way we can jump to this current index or any index after it. Therefore, since there is no way to jump to the last index, we return False.
    * We update the current max index to the maximum of itself and where we can jump to from the current index given the number at the current index (idx + nums[idx]).
    * If the updated current max index is greater than our last index, this means that we can reach the last index. Thus, we can return True.
4. If we have iterated through the nums without returning False, this means that there is a way to reach the last index. Thus, return True.

## Complexity Analysis

### Time: O(N)

We iterate through the nums array once.

### Space: O(1)

There is no extra space utilized as we keep track of one variable throughout.

## Python solution

```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:

        curr_max_index = 0

        for i in range(len(nums)):
            if i > curr_max_index:
                return False

            curr_max_index = max(curr_max_index, i + nums[i])

            if curr_max_index > len(nums) - 1:
                return True

        return True
```

## Go solution

```go
func canJump(nums []int) bool {
    curr_max_idx := 0

    for i := 0; i < len(nums); i++ {
        if i > curr_max_idx {
            return false
        }
        if i + nums[i] > curr_max_idx {
            curr_max_idx = i + nums[i]
        }
        if curr_max_idx > len(nums) - 1 {
            return true
        }
    }
    return true
}
```

## Rust solution

```rust
use std::cmp::max;

impl Solution {
    pub fn can_jump(nums: Vec<i32>) -> bool {
        let mut curr_max_idx = 0;

        for i in 0..nums.len() {
            if i > curr_max_idx {
                return false
            }
            curr_max_idx = max(curr_max_idx, i + (nums[i] as usize));
            if curr_max_idx > nums.len() - 1 {
                return true
            }
        }
        true
    }
}
```
