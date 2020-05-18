+++
title = "Counting Bits"
date = 2020-05-16
description = "Binary"
insert_anchor_links = "right"

[taxonomies]
tags = ["Binary"]
authors = ["Suzie Jung"]
+++

## How to solve

1. Initialize an answer array of size num + 1 (number of numbers from 0 to num inclusive).
2. Iterate through the answer array and fill it out.
    * The number of one bits in a given number is 1 + (the number of one bits in given number ANDed with given number minus one).
    * This holds because ANDing a number with a number one less than it flips the least significant 1-bit of the number to 0.

## Complexity Analysis

### Time: O(N)

Linear time with respect to num.

### Space: O(1)

No extra space is used.

## Python solution

```python
class Solution:
    def countBits(self, num: int) -> List[int]:
        ans = [0 for _ in range(num+1)]

        for i in range(1, num+1):
            ans[i] = ans[i&(i-1)] + 1

        return ans
```

## Go solution

```go
func countBits(num int) []int {
    ans := make([]int, num+1)
    ans[0] = 0

    for i:= 1; i < num + 1; i++ {
        ans[i] = ans[i & (i-1)] + 1
    }
    return ans
}
```

## Rust solution

```rust
impl Solution {
    pub fn count_bits(num: i32) -> Vec<i32> {
        let mut ans = vec![0; (num+1) as usize];

        for i in 1..(num+1) as usize {
            ans[i] = ans[i & (i-1)] + 1
        }

        ans
    }
}
```
