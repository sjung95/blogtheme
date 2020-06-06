+++
title = "Course Schedule"
date = 2020-05-26
description = "Graph"
insert_anchor_links = "right"

[taxonomies]
tags = ["Graph"]
authors = ["Suzie Jung"]
+++

## How to solve
The key is to use topological sort in order to detect cycles.
1. Construct a graph in which vertices are the courses and edges are the prerequisite dependencies.
    * We keep a representation of the dependencies in a hash map, where the keys are courses and the values are prerequisites needed to take the courses.
2. Next, we will check for cycles by using two sets (a visiting set - for course(s) we are currently visiting and checking if there are any cycles, and a visited set - for courses that have already been checked to not have any cycles).
3. Perform a DFS on all the courses. If we find a cycle for any of the courses, we cannot finish so we return False. Otherwise, we can finish and return True.
4. DFS:
    * We know that there is a cycle if the current course we are checking is already in the visiting set.
    * We know that we do not need to check the course we are currently checking if it is in the visited set.
    * After these checks, we add the course to the visiting set to mark it as visiting.
    * If the course is a key in the prereq dependencies hash map, we have to iterate through all its prereqs to make sure there are no cycles. So recursively call has_cycle_dfs on all its prereqs.
    * If we find a cycle, we cannot finish the courses.
    * If no cycles are found for the course we are considering, we take it out of visiting and put it in visited.

## Complexity Analysis

### Time: O(V+E)
Here, V represents the courses and E represents all the dependencies (i.e. prereq to course links). It takes V+E time to construct the hash map and in the worst case, we iterate through the whole graph, which means it takes V+E times.

### Space: O(V+E)
Our hash map (that represents the dependencies) is of size V+E.

## Python solution

```python
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        def has_cycle_dfs(course, dict_prereq, visited, visiting):
            if course in visiting:
                return True
            if course in visited:
                return False

            visiting.add(course)

            if course in dict_prereq:
                prereqs = dict_prereq[course]
                for prereq in prereqs:
                    if has_cycle_dfs(prereq, dict_prereq, visited, visiting):
                        return True

            visiting.remove(course)
            visited.add(course)

            return False


        dict_prereq = {}

        for course_pair in prerequisites:
            course = course_pair[0]
            prereq = course_pair[1]

            if course in dict_prereq:
                dict_prereq[course].append(prereq)
            else:
                dict_prereq[course] = [prereq]

        visited = set()
        visiting = set()

        for course in dict_prereq:
            if has_cycle_dfs(course, dict_prereq, visited, visiting):
                return False

        return True
```

## Go solution

```go
func canFinish(numCourses int, prerequisites [][]int) bool {
    dict_prereq := make(map[int][]int)
    for _, course_pair := range prerequisites {
        course := course_pair[0]
        prereq := course_pair[1]

        if _, in_dict := dict_prereq[course]; in_dict {
            dict_prereq[course] = append(dict_prereq[course], prereq)
        } else {
            dict_prereq[course] = []int{prereq}
        }
    }
    visited := make(map[int]bool)
    visiting := make(map[int]bool)

    for course, _ := range dict_prereq {
        if has_cycle_dfs(course, dict_prereq, visited, visiting) {
            return false
        }
    }
    return true
}

func has_cycle_dfs(course int, dict_prereq map[int][]int, visited map[int]bool, visiting map[int]bool) bool {
    if _, in_visiting := visiting[course]; in_visiting {
        return true
    }
    if _, in_visited := visited[course]; in_visited {
        return false
    }

    visiting[course] = true

    if prereqs, in_dict := dict_prereq[course]; in_dict {
        for _, prereq := range prereqs {
            if has_cycle_dfs(prereq, dict_prereq, visited, visiting) {
                return true
            }
        }
    }
    delete(visiting, course)
    visited[course] = true

    return false
}
```

## Rust Solution

```rust
use std::collections::{HashMap, HashSet};
use std::collections::hash_map::Entry;

impl Solution {
    pub fn can_finish(num_courses: i32, prerequisites: Vec<Vec<i32>>) -> bool {
        fn has_cycle_dfs(course: &i32, mut visiting: &mut HashSet<i32>, mut visited: &mut HashSet<i32>, dict_prereq: &HashMap<i32, Vec<i32>>) -> bool {
            if visiting.contains(course) {
                return true;
            }
            if visited.contains(course) {
                return false;
            }

            visiting.insert(*course);
            if dict_prereq.contains_key(course) {
                for prereq in &dict_prereq[course] {
                    if has_cycle_dfs(prereq, &mut visiting, &mut visited, &dict_prereq) {
                        return true;
                    }
                }
            }
            visiting.remove(course);
            visited.insert(*course);
            false
        }

        let mut dict_prereq: HashMap<i32, Vec<i32>> = HashMap::with_capacity(prerequisites.len());
        for course_pair in prerequisites {
            let course = course_pair[0];
            let prereq = course_pair[1];

            match dict_prereq.entry(course) {
                Entry::Vacant(entry) => { entry.insert(vec![prereq]); },
                Entry::Occupied(mut entry) => { entry.get_mut().push(prereq); }
            };
        }

        let mut visiting = HashSet::new();
        let mut visited = HashSet::new();

        for course in 0..num_courses {
            if has_cycle_dfs(&course, &mut visiting, &mut visited, &dict_prereq) {
                return false;
            }
        }
        true
    }
}
```