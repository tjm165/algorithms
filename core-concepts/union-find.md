# Union Find

[Example Leetcode](https://leetcode.com/problems/find-if-path-exists-in-graph/solutions/3678953/union-find/)

https://www.geeksforgeeks.org/union-by-rank-and-path-compression-in-union-find-algorithm/

## Description
UnionFind is a great data structure for staying organized while grouping nodes of an **undirected graph**. The data structure is composed of two operations 
1. Union: Merges two nodes together
2. Finds what relative group a node belongs to

## Intuition
We can merge two nodes together by setting one node as the parent of the other node. This way when we call `find` on each of these two nodes, they will return the same answer.

## Basic Approach
* `init` the data structure with:
   * An array `parents` such that `parents[node]` holds the parent of a given `node`. Initialize each node to be it's own parent. This can be done by a single pass through all the elements.
* `union(nodeA, nodeB)`: Will merge the two nodes together.
  * Find the roots of `nodeA`  and `nodeB`
  * Iff the two roots are not equal, then a merge must happen. Set one root to be the parent of the other root.
    * Note that in this basic approach it doesn't matter which node we set as the parent.
    * Note that if we were to always merge the nodes (even in the case that the nodes were already merged) then we would break the base case of `find`.
* `find(node)`: Will find the root of `node`. 
  * Base Case: If the node's parent is ever equal to itself, then we have found the root
  * Otherwise: Call `find` on the parent of `node`. 

## Optimized Approach
* `init` the data structure with: 
   * Rather than doing this with a single pass, let's just use defaultdict and set the default value to `-1`. We can remember that `-1` means "I am my own parent". This initialization can now be done in constant time rather than linear time.
* `find(node)`: Before, we would recursively call `find` until we got to a root. However, this could worst case take `O(n)` time! To optimize this, we can cache the result by setting `parent[node] = root`. This is called "path compression". As the algorithm runs, this will eventually lead to `find` taking `O(1)` time!

## Optimized Code

```
class UnionFind:
    def __init__(self):
        self.parent = collections.defaultdict(lambda: -1)

    # Find with path compression.
    # A path in the graph will now be on average log(n)
    def find(self, node):
        parent = self.parent[node]
        if parent == -1:
            return node
        higherAncestor = self.find(parent) # recursion
        self.parent[node] = higherAncestor # path compression
        return higherAncestor

    def union(self, a, b):
        rootA = self.find(a)
        rootB = self.find(b)

        if rootA != rootB: # else keep as -1
            self.parent[rootA] = rootB

```

## Optimized Complexity
* Time complexity
  * https://en.wikipedia.org/wiki/Disjoint-set_data_structure#Proof_of_O(log*(n))_time_complexity_of_Union-Find 
  * https://www.geeksforgeeks.org/union-find-algorithm-union-rank-find-optimized-path-compression/?ref=rp
* Space complexity: O(node)
  * We keep one array that contains one element for each node in the graph of n nodes.
  * 

# Other Operations
* Size: Must initialize a count and count down on each union
