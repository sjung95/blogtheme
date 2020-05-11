+++
title = "Three Sum"
date = 2020-05-11
description = "Array"
insert_anchor_links = "right"

[taxonomies]
tags = ["Array"]
authors = ["Suzie Jung"]
+++

## How to solve

1. Sort the nums array (needed to avoid duplicates), and initialize the ans array.
2. Iterate through nums until the third to last element. 
    * If the element is equal to the element to the left of it, go to the next iteration to avoid dups.
    * Otherwise, set left to the index after the current one and right to the last index.
    * While left < right,
        * Calculate the sum of current num, num at left and num at right.
            * If the sum is greater than 0, adjust by decreasing right.
            * If the sum is less than 0, adjust by increasing left. 
            * If the sum is zero,
                * Append the three numbers to answer array.
                * Move left to skip all duplicates.
                * Move right to skip all duplicates.
3. Return ans.

## Complexity Analysis

### Time: O(N^2)

Sorting the nums array takes NlogN time.
While iterating through the array, the for loop runs at most N times, and at each iteration we iterate through the array again (N times).

### Space: O(1)

No extra space is used.

## Python solution

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        ans = []
        nums.sort()

        for i in range(len(nums) - 2):
            if i > 0 and nums[i] == nums[i-1]:
                continue

            l = i+1
            r = len(nums) - 1

            while l < r:
                three_sum = nums[i] + nums[l] + nums[r]
                if three_sum > 0:
                    r -= 1
                elif three_sum < 0:
                    l += 1
                else:
                    ans.append([nums[i], nums[l], nums[r]])
                    while l < r and nums[l] == nums[l+1]:
                        l += 1
                    while l < r and nums[r] == nums[r-1]:
                        r -= 1
                    l += 1
                    r -= 1
        return ans
```

## Go solution

```go
func threeSum(nums []int) [][]int {
    var ans [][]int
    sort.Ints(nums)

    for i := 0; i < len(nums) - 2; i++ {
        if (i > 0) && (nums[i] == nums[i-1]) {
            continue;
        }

        l := i + 1
        r := len(nums) - 1

        for l < r {
            three_sum := nums[i] + nums[l] + nums[r]
            if three_sum > 0 {
                r -= 1
            } else if three_sum < 0 {
                l += 1
            } else {
                add_ans := make([]int, 3)
                add_ans[0] = nums[i]
                add_ans[1] = nums[l]
                add_ans[2] = nums[r]
                ans = append(ans, add_ans)

                for (l < r) && (nums[l] == nums[l+1]) {
                    l += 1
                }
                for (l < r) && (nums[r] == nums[r-1]) {
                    r -= 1
                }
                l += 1
                r -= 1
            }
        }
    }
    return ans
}
```

## Rust solution

```rust
impl Solution {
    pub fn three_sum(nums: Vec<i32>) -> Vec<Vec<i32>> {
        let mut ans = Vec::new();
        if nums.len() == 0 || nums.len() < 3 {
            return ans;
        }
        let mut nums = nums;
        nums.sort();

        for i in 0..nums.len() - 2 {
            if (i > 0) && (nums[i] == nums[i-1]) {
                continue;
            }

            let mut l = i + 1;
            let mut r = nums.len() - 1;

            while l < r {
                let mut three_sum = nums[i] + nums[l] + nums[r];
                if three_sum > 0 {
                    r -= 1
                }
                else if three_sum < 0 {
                    l += 1
                }
                else {
                    ans.push(vec![nums[i], nums[l], nums[r]]);
                    while (l < r) && (nums[l] == nums[l+1]) {
                        l += 1
                    }
                    while (l < r) && (nums[r] == nums[r-1]) {
                        r -= 1
                    }
                    l += 1;
                    r -= 1;
                }
            }
        }
        ans
    }
}
```
