+++
title = "Climbing Stairs"
date = 2020-05-18
description = "Dynamic Programming"
insert_anchor_links = "right"

[taxonomies]
tags = ["Dynamic Programming"]
authors = ["Suzie Jung"]
+++

## How to solve

1. Establish the base case for 1 and 2 steps.
    * For 1 step, there is 1 way to climb.
    * For 2 steps, there are 2 ways (1,1) or (2).
2. Use the base cases to build up to n.
    * Add the possible ways for two previous steps.
    * E.g. for 3 steps, one can either take 2 steps from 1 or 1 step from 2. Thus, the way to climb 3 steps is to add the number of ways to climb 1 step and the number of ways to climb 2 steps. 
3. Repeat until n.

## Complexity Analysis

### Time: O(N)

Linear time with respect to the number of steps to climb.

### Space: O(1)

Constant space is used to store intermediate steps. 

## Python solution

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        first = 1
        second = 2

        if n == 1:
            return first

        if n == 2:
            return second

        for i in range(2, n):
            ans = first + second
            first, second = second, ans

        return ans
```

## Go solution

```go
func climbStairs(n int) int {
    first := 1
    second := 2

    if n == 1 {
        return first
    }

    if n == 2 {
        return second
    }

    ans := 0

    for i := 2; i < n; i++ {
        ans = first + second
        first, second = second, ans
    }

    return ans
}
```

## Rust solution

```rust
impl Solution {
    pub fn climb_stairs(n: i32) -> i32 {
        let mut first = 1;
        let mut second = 2;

        if n == 1 {
            return first
        }

        if n == 2 {
            return second
        }

        let mut ans = 0;

        for i in 2..n {
            ans = first + second;
            first = second;
            second = ans;
        }

        ans
    }
}
```
