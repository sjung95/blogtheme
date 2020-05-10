+++
title = "Product of Array Except Self"
date = 2020-05-10
description = "Array"
insert_anchor_links = "right"

[taxonomies]
tags = ["Array"]
authors = ["Suzie Jung"]
+++

## How to solve

1. If nums is empty, return an empty list.
2. Perform two passes thru the array: one from left to right, and another from right to left.
    * Initialize an answer array to 1's.
    * First pass: Iterating from left to right (skipping the last element in nums), update the answer array as the product of current number and the last element in the ans array.
    * Second pass: Iterating from right to left, multiply to the current element in array the running_product.
        * Running product starts as 1, then it gets multiplied by the num in nums, right to left.
3. Return the answer array.

## Complexity Analysis

### Time: O(N)

We iterate through the array twice.

### Space: O(1)

We use constants to store the products.

## Python solution

```python
class Solution(object):
    class Solution(object):
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        if not nums:
            return []

        ans = [1 for _ in range(len(nums))]

        for i in range(len(nums) - 1):
            ans[i+1] = (ans[i] * nums[i])

        right_product = 1

        for i in range(len(nums) - 1, -1, -1):
            ans[i] *= right_product
            right_product *= nums[i]

        return ans
```

## Go solution

```go
func productExceptSelf(nums []int) []int {
    if len(nums) == 0 {
        return []int{}
    }
    ans := make([]int, len(nums))
    ans[0] = 1

    for i, num := range nums[0: len(nums)-1] {
        ans[i+1] = ans[i] * num
    }

    R := 1

    for i := range nums {
        ans[len(nums) - 1 - i] *= R
        R *= nums[len(nums) - 1 - i]
    }
    return ans
}
```

## Rust solution

```rust
impl Solution {
    pub fn product_except_self(nums: Vec<i32>) -> Vec<i32> {
        if nums.len() == 0 {
            return vec![];
        }

        let mut ans = vec![1; nums.len()];

        for i in 0..nums.len() - 1 {
            ans[i+1] = ans[i] * nums[i];
        }

        let mut R = 1;

        for i in (0..nums.len()).rev() {
            ans[i] *= R;
            R *= nums[i];
        }
        return ans;
    }
}
```
