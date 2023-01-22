[Lintcode 591 Connecting Graph III](https://www.lintcode.com/problem/591/) serves as a free alternative to [Leetcode 323. Number of Connected Components In An Undirected Graph](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/).

## Code
```
class ConnectingGraph3:
    """
    @param a: An integer
    @param b: An integer
    @return: nothing
    """
    def __init__(self, n):
        self.parents = [-1 for _ in range(n)]
        self.num_independent = n

    def find(self, nodeA):
        if self.parents[nodeA] == -1:
            return nodeA
        res = self.find(self.parents[nodeA])
        self.parents[nodeA] = res
        return res

    def connect(self, inputA, inputB):
        nodeA = inputA - 1
        nodeB = inputB - 1

        rootA = self.find(nodeA)
        rootB = self.find(nodeB)

        if rootA != rootB:
            self.num_independent -= 1

        if rootA != rootB:
            self.parents[rootA] = rootB 

    """
    @return: An integer
    """
    def query(self):
        return self.num_independent
 ```
