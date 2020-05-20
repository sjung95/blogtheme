+++
title = "Longest Increasing Subsequence"
date = 2020-05-19
description = "Dynamic Programming"
insert_anchor_links = "right"

[taxonomies]
tags = ["Dynamic Programming"]
authors = ["Suzie Jung"]
+++

## How to solve

1. The main idea is to use the greedy approach to the patience game as described in this video <https://www.youtube.com/watch?v=22s1xxRvy28&feature=youtu.be>.
2. Iterate through the nums array and make "piles" of the numbers as you would make piles of cards.
    * Rule 1: Each pile stacks numbers in decreasing order (i.e. the bottom-most number is the biggest in the pile).
    * Rule 2: Each number is put on the leftmost pile that can take the number. If a number is greater than the top number of the rightmost pile, create a new pile to the right.
3. With the two rules in place, create piles of the numbers. To keep track of the actual longest increasing subsequence, we need a separate hash map that keeps track of the connections.
    * When a card is added to a pile, update the trail_of_nums. When a new number is added to a pile, this effectively creates a pointer from this new number to the topmost (smallest) number of the previous pile if there is one.
    * To retrieve the longest increasing subsequence, backtrack from the topmost card of the rightmost pile.
4. Note that to find the proper pile to put the card, we use binary search.

## Complexity Analysis

### Time: O(NlogN)

For each of the N numbers, we have to find its proper place through binary search, which takes logN time.

### Space: O(N)

In the worst case, there are N piles (and N entries in the hashmap that keeps track of the pointers - this data structure is optional as it is not required by the problem to return the actual subsequence).
    * This would happen if nums was in a strictly increasing order.

## Python solution

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        if not nums:
            return 0

        piles = []
        trail_of_nums = {}

        for num in nums:
            if not piles or num > piles[-1]:
                piles.append(num)

                if len(piles) > 1:
                    trail_of_nums[num] = piles[-2]

            else:
                left = 0
                right = len(piles) - 1

                while left <= right:
                    mid = left + (right-left)//2

                    if piles[mid] < num:
                        left = mid + 1
                    else:
                        right = mid - 1

                piles[left] = num
                if left != 0:
                    trail_of_nums[num] = piles[left-1]

        ptr = piles[-1]
        back_ptrs = []
        while ptr in trail_of_nums:
            back_ptrs.append(ptr)
            ptr = trail_of_nums[ptr]

        back_ptrs.append(ptr)
        print(list(reversed(back_ptrs)))
        return len(piles)
```

## Go solution

```go
func lengthOfLIS(nums []int) int {
    if len(nums) == 0 {
        return 0
    }

    var piles [] int
    trail_of_nums := make(map[int]int)

    for _, num := range nums {
        if (len(piles) == 0) || num > piles[len(piles) - 1] {
            piles = append(piles, num)
            if len(piles) > 1 {
                trail_of_nums[num] = piles[len(piles) - 2]
            }
        } else {
            left := 0
            right := len(piles) - 1

            for left <= right {
                mid := left + (right-left)/2

                if piles[mid] < num {
                    left = mid + 1
                } else {
                    right = mid - 1
                }
            }
            piles[left] = num

            if left != 0 {
                trail_of_nums[num] = piles[left-1]
            }
        }
    }

    ptr := piles[len(piles) - 1]
    var back_ptrs [] int
    for {
        back_ptrs = append(back_ptrs, ptr)
        value, exists := trail_of_nums[ptr]
        if exists {
            ptr = value
        } else {
            break
        }
    }
    fmt.Printf("%v", back_ptrs)
    return len(piles)
}
```

## Rust solution

```rust
use std::collections::HashMap;

impl Solution {
    pub fn length_of_lis(nums: Vec<i32>) -> i32 {
        if nums.len() == 0 {
            return 0;
        }
        let mut piles = Vec::new();
        let mut trail_of_nums = HashMap::new();

        for num in &nums {
            if (piles.len() == 0) || (num > piles[piles.len() -1]) {
                piles.push(num);

                if piles.len() > 1 {
                    trail_of_nums.insert(num, piles[piles.len() - 2]);
                }
            }
            else {
                let mut left = 0 as i32;
                let mut right = (piles.len() -1) as i32;

                while left <= right {
                    let mut mid = (left + (right-left) / 2) as usize;
                    if piles[mid] < num {
                        left = (mid + 1) as i32;
                    }
                    else {
                        right = (mid - 1) as i32;
                    }
                }

                piles[left as usize] = num;
                if left != 0 {
                    trail_of_nums.insert(num, piles[(left-1) as usize]);
                }
            }
        }
        let mut ptr = piles[piles.len() - 1];
        let mut back_ptrs = Vec::with_capacity(piles.len());
        loop {
            back_ptrs.push(ptr);
            match trail_of_nums.get(ptr) {
                Some(previous_num) => {
                    ptr = previous_num;
                },
                None => break
            };
        }
        println!("{:?}", back_ptrs);
        return (piles.len() as i32)
    }
}
```
