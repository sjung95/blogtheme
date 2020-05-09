+++
title = "Two Sum"
date = 2020-05-09
description = "Array"
insert_anchor_links = "right"

[taxonomies]
tags = ["Array"]
authors = ["Suzie Jung"]
+++

## How to solve

1. Create a hash table in which the index is the number and the value is the index of the number in the array.
2. Iterate through the array to populate the hash table while also checking for the complement that adds to the target.
3. Return the indices of numbers that sum to target.

## Complexity Analysis

### Time: O(N)

We iterate through the array once. 

### Space: O(N)

We store all the numbers and its index in the worst case (if no two numbers sum to target).

## Python solution

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        target_dict = {}

        for i, num in enumerate(nums):
            comp = target - num 
            if comp in target_dict: 
                return [target_dict[comp], i]
            else:
                target_dict[num] = i 
```

