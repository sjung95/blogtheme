+++
title = "Find Minimum in a Rotated Sorted Array"
date = 2020-05-11
description = "Array"
insert_anchor_links = "right"

[taxonomies]
tags = ["Array"]
authors = ["Suzie Jung"]
+++

## How to solve

1. We will perform a binary search.
2. Set lo to 0 and hi to the last index.
3. If array is already in sorted order, return the first element.
4. Otherwise, search for the minimum.
    * Set mid to the middle of lo and hi. 
    * If nums[mid] is greater than nums[mid+1], mid+1 is our min. Return.
    * If nums[mid] is less than nums[mid-1], mid is our min. Return.
    * Otherwise, adjust lo or hi.
        * If nums[mid] > nums[lo], we need to search the right of mid. So set lo = mid + 1.
        * If nums[mid] < nums[hi], we need to search the left of mid. So set hi = mid - 1.
5. Set default return to nums[lo].

## Complexity Analysis

### Time: O(logN)

We binary search the array.

### Space: O(1)

We do not use extra space.

## Python solution

```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        lo = 0
        hi = len(nums) - 1

        if nums[hi] >= nums[lo]:
            return nums[lo]

        while lo <= hi:
            mid = lo + (hi - lo) // 2
            if nums[mid] > nums[mid+1]:
                return nums[mid+1]
            if nums[mid] < nums[mid-1]:
                return nums[mid]
            if nums[mid] > nums[lo]:
                lo = mid + 1
            if nums[mid] < nums[hi]:
                hi = mid - 1

        return nums[lo]

```

## Go solution

```go
func findMin(nums []int) int {
    lo := 0
    hi := len(nums) - 1

    if nums[hi] >= nums[lo] {
        return nums[lo]
    }

    for lo <= hi {
        mid := lo + (hi - lo) / 2
        if nums[mid] > nums[mid+1] {
            return nums[mid+1]
        }
        if nums[mid] < nums[mid-1] {
            return nums[mid]
        }
        if nums[lo] < nums[mid] {
            lo = mid + 1
        }
        if nums[hi] > nums[mid]  {
            hi = mid - 1
        }
    }
    return nums[lo]
}
```

## Rust solution

```rust
impl Solution {
    pub fn find_min(nums: Vec<i32>) -> i32 {
        let mut lo = 0;
        let mut hi = nums.len() - 1;

        if nums[hi] >= nums[lo] {
            return nums[lo]
        }

        while lo <= hi {
            let mut mid = lo + (hi - lo) / 2;

            if nums[mid] > nums[mid + 1] {
                return nums[mid+1]
            }
            if nums[mid] < nums[mid - 1] {
                return nums[mid]
            }
            if nums[mid] > nums[lo] {
                lo = mid + 1
            }
            if nums[hi] > nums[mid] {
                hi = mid - 1
            }
        }
        nums[lo]
    }
}
```
