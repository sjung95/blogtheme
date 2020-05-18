+++
title = "Missing Number"
date = 2020-05-16
description = "Binary"
insert_anchor_links = "right"

[taxonomies]
tags = ["Binary"]
authors = ["Suzie Jung"]
+++

## How to solve

1. Set the answer to n (length of nums array).
2. XOR n with the index and value of every element in the nums array.
3. This yields the missing number.

## Complexity Analysis

### Time: O(N)

The algorithm iterates through the nums array once; thus,assuming XOR is a constant-time operation, the runtime is linear.

### Space: O(1)

Only constant space is used.

## Python solution

```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        ans = len(nums)

        for i, num in enumerate(nums):
            ans ^= i ^ num

        return ans
```

## Go solution

```go
func missingNumber(nums []int) int {
    ans := len(nums)

    for i, num := range nums {
        ans ^= i ^ num
    }
    return ans
}
```

## Rust solution

```rust
impl Solution {
    pub fn missing_number(nums: Vec<i32>) -> i32 {
        let mut ans = nums.len();

        for i in 0..nums.len()  {
            ans ^= (nums[i] as usize) ^ i;
        }
        ans as i32
    }
}
```
