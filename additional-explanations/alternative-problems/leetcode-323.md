[Lintcode 591 Connecting Graph III](https://www.lintcode.com/problem/591/) serves as a free alternative to [Leetcode 323. Number of Connected Components In An Undirected Graph](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/).

# Intuitiion
The problem states that we need to count the number of connected components in an **undirected graph**. Because this is undirected, we can use the UnionFind datastructure. Furthermore, reading the prompt and given method stubs, it is clear that we are expected to implement union find. More specifically, we will actually need to fine tune the performance of a standard union find to use "path compression".

The intuition behind union find is to recursively ask each node who its parent is until you reach a node. In this explanation I will discuss how we get UnionFind to fit this problem. For a more detailed explanation of the UnionFind data structure I recommend reading my [UnionFind explanation](https://github.com/tjm165/algorithms-practice/blob/main/additional-explanations/union-find.md)

After implementing UnionFind, we need to consider how to count how many connected components there are. We have two options, we can either count all at once, or we can count as we go. Counting as we go is much more efficient and thus we will choose this option.

# Code
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
