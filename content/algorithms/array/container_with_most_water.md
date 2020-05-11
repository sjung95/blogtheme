+++
title = "Container with Most Water"
date = 2020-05-11
description = "Array"
insert_anchor_links = "right"

[taxonomies]
tags = ["Array"]
authors = ["Suzie Jung"]
+++

## How to solve

1. Initialize max_area to 0 and set lo to 0 and hi to the last index of height.
2. Update the max_area to be a max of max area and area set by current lo and hi.
3. Update lo or hi: move the smaller of the two towards the middle (inward).
4. Return max area.

## Complexity Analysis

### Time: O(N)

We consider each element in the height array.

### Space: O(1)

No extra space is used.

## Python solution

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:

        max_area = 0
        lo = 0
        hi = len(height) - 1

        while lo < hi:
            max_area = max(max_area, min(height[lo], height[hi]) * (hi - lo))
            if height[lo] < height[hi]:
                lo += 1
            else:
                hi -= 1

        return max_area
```

## Go solution

```go
func maxArea(height []int) int {
    max_area := 0
    lo := 0
    hi := len(height) - 1

    for lo < hi {
        max_area = max(max_area, min(height[lo], height[hi])*(hi-lo))
        if height[lo] < height[hi] {
            lo += 1
        } else {
            hi -= 1
        }
    }
    return max_area
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
    pub fn max_area(height: Vec<i32>) -> i32 {
        // problem statement says height will have at least 2 numbers
        let mut max_area = 0;
        let mut lo = 0;
        let mut hi = height.len() - 1;

        while lo < hi {
            max_area = max(max_area, min(height[lo], height[hi])*((hi-lo) as i32));
            if height[lo] < height[hi] {
                lo += 1
            }
            else {
                hi -= 1
            }
        }
        return max_area
    }
}
```
