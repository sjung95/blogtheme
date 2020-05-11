+++
title = "Contains Duplicates"
date = 2020-05-10
description = "Array"
insert_anchor_links = "right"

[taxonomies]
tags = ["Array"]
authors = ["Suzie Jung"]
+++

## How to solve

1. Create a set that will store the num in nums.
2. Iterate through the array nums.
    * If the num is already in the set, it is a duplicate. Return True.
    * Otherwise, we have not seen the num before, so add to the set. 
3. Return False.

## Complexity Analysis

### Time: O(N)

We iterate through the array once.

### Space: O(N)

We store all the numbers in the worst case (if there are no duplicates).

## Python solution

```python
class Solution(object):
    def containsDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        set_nums = set()

        for num in nums:
            if num in set_nums:
                return True
            else:
                set_nums.add(num)

        return False
```

## Go solution

```go
func containsDuplicate(nums []int) bool {
    set := make(map[int]bool)

    for _, num := range nums {
        _, in_set := set[num]
        if in_set {
            return true
        }
        set[num] = true
    }
    return false
}
```

## Rust solution

```rust
use std::collections::HashSet;

impl Solution {
    pub fn contains_duplicate(nums: Vec<i32>) -> bool {
        let mut set_nums = HashSet::with_capacity(nums.len());
        for &num in &nums {
            if set_nums.contains(&num) {
                return true
            }
            set_nums.insert(num);
        }

        false  
    }
}
```
