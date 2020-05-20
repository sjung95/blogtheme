+++
title = "Word Break"
date = 2020-05-20
description = "Dynamic Programming"
insert_anchor_links = "right"

[taxonomies]
tags = ["Dynamic Programming"]
authors = ["Suzie Jung"]
+++

## How to solve

1. To check whether the given string s can be made up of the strings in the dictionary, we divide the string s into substrings and check whether the substrings are present in the dictionary.
2. To do this, we use a dp array of size len(s) + 1 and utilize two pointers (i and j).
    * First, set the base case of a null string.  dp[0] = True.
    * Then, we iterate through the string and check if s[0:i] is in the dictionary. If it is (dp array should be set to True at that index), we check whether the rest of string s can be made of up words in the dictionary.
    * Pointer j moves through the rest of the string if applicable and checks s[i:j+1) is present in the dictionary and updates dp[j+1] to be True.

## Complexity Analysis

### Time: O(N*2)

N = len(s). In the worst case, for the 1st, 2nd, 3rd... last character, we iterate through (n-1), (n-2), .... 1 characters. This sums to n*2 per Gauss's formula.

### Space: O(N) or O(len(wordDict))

We utilize a dp array of len(s) + 1 = N + 1 = O(N).
We also create a hash set of the given wordDict.

## Python solution

```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:

        dp = [False for _ in range(len(s) + 1)]

        dp[0] = True

        word_set = set(wordDict)

        for i in range(len(s)):
            if dp[i]:
                for j in range(i, len(s)):
                    if s[i:j+1] in word_set:
                        dp[j+1] = True

        return dp[-1]
```

## Go solution

```go
func wordBreak(s string, wordDict []string) bool {
    dp := make([]bool, len(s)+1)
    word_set := make(map[string]struct{})

    for _, val := range wordDict {
        word_set[val] = struct{}{}
    }

    dp[0] = true

    for i := 0; i <  len(s); i++ {
        if dp[i] {
            for j := i; j < len(s); j++ {
                _, exists := word_set[s[i:j+1]]
                if exists {
                    dp[j+1] = true
                }
            }
        }
    }
    return dp[len(s)]
}
```

## Rust solution

```rust
use std::collections::HashSet;

impl Solution {
    pub fn word_break(s: String, word_dict: Vec<String>) -> bool {
        let mut dp = vec![false; s.len() + 1];
        let mut word_set: HashSet<String> = HashSet::with_capacity(word_dict.len());

        for word in word_dict {
            word_set.insert(word);
        }

        dp[0] = true;

        for i in 0..s.len() {
            if dp[i] {
                for j in i..s.len() {
                    if word_set.contains(&s[i..j+1]) {
                        dp[j+1] = true;
                    }
                }
            }
        }
        dp[s.len()]
    }
}
```
