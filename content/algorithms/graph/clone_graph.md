+++
title = "Clone Graph"
date = 2020-05-26
description = "Graph"
insert_anchor_links = "right"

[taxonomies]
tags = ["Dynamic Programming"]
authors = ["Suzie Jung"]
+++

## How to solve

1. Initialize a queue that will contain the nodes that we visit that have yet to be cloned.
    * Add the passed-in node to the queue.
2. Create a hashmap with key as the old node and the value as the cloned node.
    * Create a clone of the passed-in node and insert the pairing into the hashmap.
3. Now, utilize a BFS to visit the neighbors.
    * To perform this BFS exhaustively, use a while loop. The condition being checked is whether the queue is empty, as this queue holds nodes that have been visited but not yet cloned.
    * Thus in the while loop, we "pop" from the queue.
        * In the case of python, we can use a deque and pop left but we can also just use a normal pop of a list because we will never clone the same node twice or mess up the order since we check for whether we have visited that node by checking if the node is a key in the hashmap and by performing a BFS.
    * For the popped node, iterate through all its neighbors. If a neighbor is not in the hashmap, add it with the clone of it as the value and empty neighbors list. Then append the neighbor to the queue. Append the cloned neighbor to the neighbors list of the current cloned node we are considering.
4. Return the copy of the passed-in node.

## Complexity Analysis

### Time: O(N)

Linear time with respect to the number of nodes in a graph. We only check and clone each node once.

### Space: O(N)

The size of the queue can be at most n - 1. Do we include the space of the hashmap?

## Python solution

```python
class Solution:
    def cloneGraph(self, node: 'Node') -> 'Node':
        if not node:
            return None

        queue = [node]
        visited = {}
        visited[node] = Node(node.val, [])

        while queue:
            curr_node = queue.pop()

            for neighbor in curr_node.neighbors:
                if neighbor not in visited:
                    visited[neighbor] = Node(neighbor.val, [])
                    queue.append(neighbor)
                visited[curr_node].neighbors.append(visited[neighbor])

        return visited[node]
```

## Go solution

```go
func cloneGraph(node *Node) *Node {
    if node == nil {
        return nil
    }

    visited := make(map[int]*Node)
    new_node := &Node{Val: node.Val}
    visited[node.Val] = new_node
    queue := []*Node{node}

    for len(queue) > 0 {
        curr := queue[0]
        queue = queue[1:]

        for _, nbhr := range curr.Neighbors {
            _, in_visited := visited[nbhr.Val]
            if !in_visited {
                visited[nbhr.Val] = &Node{Val: nbhr.Val}
                queue = append(queue, nbhr)
            }
            visited[curr.Val].Neighbors = append(visited[curr.Val].Neighbors, visited[nbhr.Val])
        }
    }
    return new_node
}
```
