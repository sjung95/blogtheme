+++
title = "Reverse Bits"
date = 2020-05-16
description = "Binary"
insert_anchor_links = "right"

[taxonomies]
tags = ["Binary"]
authors = ["Suzie Jung"]
+++

## How to solve

1. Use the divide and conquer approach.
    * Assuming the input number is 32 bits, start reversing by swapping the first 16 bits with the last 16 bits.
    * Then for each 16 bit half, swap the first 8 bits with the last 8 bits. Repeat for each 4 bit group, 2 bit group, and then 1 bit.

## Complexity Analysis

### Time: O(NlogN)

This is derived from using the second case of Master's Theorem.
The number of sub-problems is a=2. The size of each sub-problem is n/b=n/2. The cost of work that has to be done is f(n)=n to flip the bits at every level.

### Space: O(1)

No extra space is used.

## Python solution

```python
class Solution:
    def reverseBits(self, n: int) -> int:

        n = ((0xFFFF0000 & n) >> 16) | ((0x0000FFFF & n) << 16)
        n = ((0xFF00FF00 & n) >> 8) | ((0x00FF00FF & n) << 8)
        n = ((0xF0F0F0F0 & n) >> 4) | ((0x0F0F0F0F & n) << 4)
        n = ((0xcccccccc & n) >> 2) | ((0x33333333 & n) << 2)
        n = ((0xaaaaaaaa & n) >> 1) | ((0x55555555 & n) << 1)

        return n
```

## Go solution

```go
func reverseBits(num uint32) uint32 {
        num = ((0xFFFF0000 & num) >> 16) | ((0x0000FFFF & num) << 16)
        num = ((0xFF00FF00 & num) >> 8) | ((0x00FF00FF & num) << 8)
        num = ((0xF0F0F0F0 & num) >> 4) | ((0x0F0F0F0F & num) << 4)
        num = ((0xcccccccc & num) >> 2) | ((0x33333333 & num) << 2)
        num = ((0xaaaaaaaa & num) >> 1) | ((0x55555555 & num) << 1)

        return num
}
```
