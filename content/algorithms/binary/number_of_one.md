+++
title = "Number of 1 Bits"
date = 2020-05-14
description = "Binary"
insert_anchor_links = "right"

[taxonomies]
tags = ["Binary"]
authors = ["Suzie Jung"]
+++

## How to solve

1. Flip the least significant 1-bit to 0.
    * To do this, AND n with n-1.
2. Add 1 to the count of number of 1 bits.
3. Repeat this until n is 0.

## Complexity Analysis

### Time: O(N)

Linear time with respect to the number of bits. In the worst case, if every bit is 1, we will have to iterate N times.

### Space: O(1)

No extra space is used.

## Python solution

```python
class Solution:
    def hammingWeight(self, n: int) -> int:
        num_of_one = 0

        while n:
            n &= n - 1
            num_of_one += 1

        return num_of_one
```

## Go solution

```go
func hammingWeight(num uint32) int {
    num_of_one := 0

    for num != 0 {
        num = num&(num-1)
        num_of_one += 1
    }

    return num_of_one
}
```

## Rust solution

```rust
impl Solution {
    pub fn hammingWeight (n: u32) -> i32 {
        let mut num = n;
        let mut num_one = 0;
        while num != 0 {
            let temp = num&(num-1);
            num = temp;
            num_one += 1;
        }
        return num_one;
    }
}
```
