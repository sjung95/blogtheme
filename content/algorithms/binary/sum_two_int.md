+++
title = "Sum Two Integers"
date = 2020-05-12
description = "Binary"
insert_anchor_links = "right"

[taxonomies]
tags = ["Binary"]
authors = ["Suzie Jung"]
+++

## How to solve

* For Python

1. Since python has infinite bit representation, we need to keep track of only the last 32 bits. To do this, we will use a mask (which is 32 1 bits) and a max_positive number, which is the maximum positive number possible in 32 bit system (this max_pos number has 31 1 bits).

2. In a while loop, we will compute the sum. This is done by XORing a and b (then ANDing with the mask to keep only the last 32 bits), and ANDing a and b then left shifting by 1 (this is done to keep track of the carry). Then this is also ANDed with the mask to keep the last 32 bits.

3. When there is no carry, we can return our answer.
    * If a is less than or equal to the max possible number, we can simply return a.
    * Otherwise, we need to return the negative number represented by a (i.e. the sign bit (the leftmost bit is set to 1)). To do so, we need to use tilde. ~ flips the bits and reads the number as negative. However, we do not need to flip the bits since a is already negative. Thus, we simply flip a's bits first by XORing a with the mask before using ~.

* For Go, Rust

1. The idea is largely the same as the python solution. We do not need the mask or the max pos variable.

## Complexity Analysis

### Time: O(1)

Unsure ...

### Space: O(1)

No extra space is used.

## Python solution

```python
class Solution:
    def getSum(self, a: int, b: int) -> int:
        mask = 2**32 - 1
        max_pos = 2**31 - 1

        while b:
            a, b = (a^b) & mask, ((a&b) << 1) & mask

        if a <= max_pos:
            return a
        else:
            return ~(a^mask)
```

## Go solution

```go
func getSum(a int, b int) int {
    for b != 0 {
        a, b = (a^b), (a&b) << 1
    }
    return a
}
```

## Rust solution

```rust
impl Solution {
    pub fn get_sum(a: i32, b: i32) -> i32 {
        let mut sum = a;
        let mut carry = b;

        while carry != 0 {
            let new_sum = sum^carry;
            let new_carry = (sum&carry) << 1;

            sum = new_sum;
            carry = new_carry;
        }
        sum
    }
}
```
