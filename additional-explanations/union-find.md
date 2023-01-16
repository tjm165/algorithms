# Union Find

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
* `union(nodeA, nodeB)` will set `nodeA` as the parent of `nodeB`. Note that in this basic approach it doesn't matter which node we set as the parent.
* `find(node)` will recursively call itself on the parent of `node`. This will continue until we find a node that is it's own parent.

## Optimized Approach
* `init` the data structure with: 
   * Rather than doing this with a single pass, let's just use defaultdict and set the default value to `-1`. We can remember that `-1` means "I am my own parent". This initialization can now be done in constant time rather than linear time.
   * An array `rank` such that `rank[node]` will tell us the rank of this `node`. This will lead to an optimization in `union`. 
* `union(nodeA, nodeB)`: 
   * Before we said, that it did not matter which node was the parent. However, this could risk leading to a giant linked-list-like-path of size `n`. By setting the node with the larger rank as the parent node, we prevent the path from ever exceeding size `log(n)`. 
* `find`

```

```

## Optimized Complexity
* Time complexity
   * https://www.geeksforgeeks.org/union-find-algorithm-union-rank-find-optimized-path-compression/?ref=rp
* Space complexity
