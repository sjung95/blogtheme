+++
title = "Search in Rotated Sorted Array"
date = 2020-05-11
description = "Array"
insert_anchor_links = "right"

[taxonomies]
tags = ["Array"]
authors = ["Suzie Jung"]
+++

## How to solve

1. We will perform a binary search.
    * If nums is invalid, return -1.
2. Set lo to 0 and hi to the last index.
3. Search for the target.
    * Set mid to the middle of lo and hi.
    * If nums[mid] is target, return mid.
    * Otherwise, adjust lo or hi.
        * If nums[lo] <= nums[mid],
            * If target is between the two, adjust hi to mid - 1.
            * Else, adjust lo to mid + 1.
        * Else
            * If target is between mid and hi, adjust lo to mid + 1.
            * Else, adjust hi to mid - 1.
        * If nums[mid] < nums[hi], we need to search the left of mid. So set hi = mid - 1.
4. Return -1.

## Complexity Analysis

### Time: O(logN)

We binary search the array.

### Space: O(1)

We do not use extra space.

## Python solution

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        if not nums:
            return -1

        lo = 0
        hi = len(nums) - 1

        while lo <= hi:
            mid = lo + (hi - lo) // 2

            if nums[mid] == target:
                return mid

            if nums[lo] <= nums[mid]:
                if nums[lo] <= target <= nums[mid]:
                    hi = mid - 1
                else:
                    lo = mid + 1
            else:
                if nums[mid] <= target <= nums[hi]:
                    lo = mid + 1
                else:
                    hi = mid - 1

        return -1
```

## Go solution

```go
func search(nums []int, target int) int {
    if len(nums) == 0 {
        return -1
    }

    lo := 0
    hi := len(nums) - 1

    for lo <= hi {
        mid := lo + (hi - lo) / 2
        if nums[mid] == target {
            return mid
        }

        if nums[lo] <= nums[mid] {
            if (nums[lo] <= target) && (target <= nums[mid]) {
                hi = mid - 1
            } else {
                lo = mid + 1
            }
        } else {
            if (nums[mid] <= target) && (target <= nums[hi]) {
                lo = mid + 1
            } else {
                hi = mid - 1
            }
        }
    }
    return -1
}
```

## Rust solution

```rust
impl Solution {
    pub fn search(nums: Vec<i32>, target: i32) -> i32 {
        if nums.len() == 0 {
            return -1
        }
        let mut lo = 0;
        let mut hi = nums.len() - 1;

        while lo <= hi {
            let mut mid = lo + (hi - lo) / 2;
            if nums[mid] == target {
                return mid as i32
            }

            if nums[lo] <= nums[mid] {
                if (nums[lo] <= target) && (target <= nums[mid]) {
                    hi = mid - 1
                }
                else {
                    lo = mid + 1
                }
            }
            else {
                if (nums[mid] <= target) && (target <= nums[hi]) {
                    lo = mid + 1
                }
                else {
                    hi = mid - 1
                }
            }
        }
        -1
    }
}
```
