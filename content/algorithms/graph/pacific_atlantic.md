+++
title = "Pacific Atlantic Water Flow"
date = 2020-06-06
description = "Graph"
insert_anchor_links = "right"

[taxonomies]
tags = ["Graph"]
authors = ["Suzie Jung"]
+++

## How to solve

1. Initialize two boolean 2d arrays with the same dimension as the matrix. Each will represent whether each cell can reach each ocean.
2. We utilize depth first search. Start from a cell we know can reach the pacific ocean (or the atlantic ocean) and mark that cell for the ocean to true. Then dfs to all its neighbors (the four directions - left, right, up, and down) that are reachable to the given ocean.
    * We do not blindly check for all the four directions. We check whether the directions are in bound, and if the cell is worth checking. The neighboring cell is worth checking only if it is marked as false (i.e. if it is marked as true, no need to check again) and if in the matrix the neighboring cell has a value greater than or equal to the current cell (condition of the problem).
3. After the dfs is done, iterate through the two boolean 2d arrays. If the values at the indices are true for both oceans, it means that cell can reach both oceans. Append the indices to the answer.

## Complexity Analysis

### Time: O(N)
N denotes the number of cells in the matrix. At most we visit all the cells in the matrix once per ocean. We do not visit cells we have already visited before.

### Space: O(N)
We use two arrays of size N for the two oceans to mark each cell's ability to flow to the ocean. Also, the recursive stack can grow at most to N (the number of cells). So O(2*N + N) = O(N).

## Python solution

```python
class Solution:
    def pacificAtlantic(self, matrix: List[List[int]]) -> List[List[int]]:
        if not matrix:
            return []

        def dfs(ocean, row, col):
            ocean[row][col] = True

            if row > 0 and not ocean[row-1][col] and matrix[row-1][col] >= matrix[row][col]:
                dfs(ocean, row-1, col)
            if row < rows - 1 and not ocean[row+1][col] and matrix[row+1][col] >= matrix[row][col]:
                dfs(ocean, row+1, col)
            if col > 0 and not ocean[row][col-1] and not ocean[row][col-1] and matrix[row][col-1] >= matrix[row][col]:
                dfs(ocean, row, col-1)
            if col < cols - 1 and not ocean[row][col+1] and matrix[row][col+1] >= matrix[row][col]:
                dfs(ocean, row, col+1)

        rows = len(matrix)
        cols = len(matrix[0])

        pacific = [[False for _ in range(cols)] for _ in range(rows)]
        atlantic = [[False for _ in range(cols)] for _ in range(rows)]

        for row in range(rows):
            dfs(pacific, row, 0)
            dfs(atlantic, row, cols-1)
        for col in range(cols):
            dfs(pacific, 0, col)
            dfs(atlantic, rows-1, col)

        ans = []

        for r in range(rows):
            for c in range(cols):
                if pacific[r][c] and atlantic[r][c]:
                    ans.append([r, c])

        return ans
```

## Go solution

```go
func pacificAtlantic(matrix [][]int) [][]int {
    if len(matrix) == 0 || len(matrix[0]) == 0 {
        return nil
    }

    rows := len(matrix)
    cols := len(matrix[0])

    pacific := make([][]bool, rows)
    atlantic := make([][]bool, rows)
    for i := 0; i < rows; i++ {
        pacific[i] = make([]bool, cols)
        atlantic[i] = make([]bool, cols)
    }

    for i := 0; i < rows; i++ {
        dfs(matrix, pacific, i, 0)
        dfs(matrix, atlantic, i, cols-1)
    }
    for j := 0; j < cols; j++ {
        dfs(matrix, pacific, 0, j)
        dfs(matrix, atlantic, rows-1, j)
    }
    ans := [][]int{}
    for i := 0; i < rows; i++ {
        for j := 0; j < cols; j++ {
            if pacific[i][j] && atlantic[i][j] {
                ans = append(ans, []int{i, j})
            }
        }
    }
    return ans
}

func dfs(matrix [][]int, ocean [][]bool, row int, col int) {
    ocean[row][col] = true
    rows := len(matrix)
    cols := len(matrix[0])

    if (row > 0) && (!ocean[row-1][col]) && (matrix[row-1][col] >= matrix[row][col]) {
        dfs(matrix, ocean, row-1, col)
    }
    if (row < rows-1) && (!ocean[row+1][col]) && (matrix[row+1][col] >= matrix[row][col]) {
        dfs(matrix, ocean, row+1, col)
    }
    if (col > 0) && (!ocean[row][col-1]) && (matrix[row][col-1] >= matrix[row][col]) {
        dfs(matrix, ocean, row, col-1)
    }
    if (col < cols-1) && (!ocean[row][col+1]) && (matrix[row][col+1] >= matrix[row][col]) {
        dfs(matrix, ocean, row, col+1)
    }
}
```

## Rust Solution

```rust
impl Solution {
    pub fn pacific_atlantic(matrix: Vec<Vec<i32>>) -> Vec<Vec<i32>> {
        fn dfs(matrix: &Vec<Vec<i32>>, mut ocean: &mut Vec<Vec<bool>>, row: usize, col: usize) {
            ocean[row][col] = true;
            let rows = matrix.len();
            let cols = matrix[0].len();

            if row > 0 && (!ocean[row-1][col]) && (matrix[row-1][col] >= matrix[row][col]) {
                dfs(&matrix, &mut ocean, row-1, col);
            }
            if row < rows-1 && (!ocean[row+1][col]) && (matrix[row+1][col] >= matrix[row][col]) {
                dfs(&matrix, &mut ocean, row+1, col);
            }
            if col > 0 && (!ocean[row][col-1]) && (matrix[row][col-1] >= matrix[row][col]) {
                dfs(&matrix, &mut ocean, row, col-1);
            }
            if col < cols-1 && (!ocean[row][col+1]) && (matrix[row][col+1] >= matrix[row][col]) {
                dfs(&matrix, &mut ocean, row, col+1);
            }
        }

        if matrix.len() == 0 || matrix[0].len() == 0 {
            return Vec::new();
        }
        let rows = matrix.len();
        let cols = matrix[0].len();

        let mut pacific: Vec<Vec<bool>> = Vec::with_capacity(rows);
        let mut atlantic: Vec<Vec<bool>> = Vec::with_capacity(rows);
        for i in 0..rows {
            pacific.push(vec![false;cols]);
            atlantic.push(vec![false;cols]);
        }

        for i in 0..rows {
            dfs(&matrix, &mut pacific, i, 0);
            dfs(&matrix, &mut atlantic, i, cols-1);
        }
        for j in 0..cols {
            dfs(&matrix, &mut pacific, 0, j);
            dfs(&matrix, &mut atlantic, rows-1, j);
        }
        let mut ans: Vec<Vec<i32>> = Vec::new();
        for i in 0..rows {
            for j in 0..cols {
                if pacific[i][j] && atlantic[i][j] {
                    ans.push(vec![i as i32, j as i32]);
                }
            }
        }
        ans
    }
}
```