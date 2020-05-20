+++
title = "Combination Sum IV"
date = 2020-05-20
description = "Dynamic Programming"
insert_anchor_links = "right"

[taxonomies]
tags = ["Dynamic Programming"]
authors = ["Suzie Jung"]
+++

## How to solve

1. Create a dp array of length target+1 with values initialized to 0s. The value at an index of the dp array denotes the possible ways to sum to the index amount.
2. Set the base case: dp[0] = 1. There is 1 way to sum to 0, which is accomplished by using 0 numbers.
3. Iterate through the dp array starting from index 1, and for each target amount specified by the dp array index, we iterate through the nums and add possible ways to sum to the amount.
    * If the given index (our target amount at a given step) is greater than or equal to the current number, we can add to the ways to make the current amount the ways to make the current amount - current number.
4. Return the last element in the dp array.

## Complexity Analysis

### Time: O((target)*len(nums))

For each character in target, we iterate through the nums array entirely.

### Space: O(target)

We utilize a dp array of length target + 1. 

## Python solution

```python
class Solution:
    def combinationSum4(self, nums: List[int], target: int) -> int:
        dp = [0 for _ in range(target+1)]
        dp[0] = 1

        for i in range(1, target+1):
            for num in nums:
                if i >= num:
                    dp[i] += dp[i-num]

        return dp[-1]
```

## Go solution

```go
func combinationSum4(nums []int, target int) int {
    dp := make([]int, target+1)
    dp[0] = 1

    for i := 0; i < target+1; i++ {
        for _, num := range nums {
            if i >= num {
                dp[i] += dp [i-num]
            }
        }
    }
    return dp[target]
}
```

## Rust solution

```rust
impl Solution {
    pub fn combination_sum4(nums: Vec<i32>, target: i32) -> i32 {
        let mut dp = vec![0; (target+1) as usize];
        dp[0] = 1;

        for i in 0..target+1 {
            for &num in &nums {
                if i >= num {
                    dp[i as usize] += dp[(i-num) as usize]
                }
            }
        }

        dp[target as usize]
    }
}
```
