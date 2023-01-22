[Lintcode 591 Connecting Graph III](https://www.lintcode.com/problem/591/) serves as a free alternative to [Leetcode 323. Number of Connected Components In An Undirected Graph](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/).

# Intuitiion
The problem states that we need to count the number of connected components in an **undirected graph**. Because this is undirected, we can use the UnionFind datastructure. Furthermore, reading the prompt and given method stubs, it is clear that we are expected to implement union find. More specifically, we will actually need to fine tune the performance of a standard union find to use "path compression".

The intuition behind union find is to recursively ask each node who its parent is until you reach a node. In this explanation I will discuss how we get UnionFind to fit this problem. For a more detailed explanation of the UnionFind data structure I recommend reading my [UnionFind explanation](https://github.com/tjm165/algorithms-practice/blob/main/additional-explanations/union-find.md)

After implementing UnionFind, we need to consider how to count how many connected components there are. We have two options, we can either count all at once, or we can count as we go. Counting as we go is much more efficient and thus we will choose this option. More specifically, we will assume we start with N independent islands and then count down everytime we merge two islands together.

# Approach
* `init`: We will initialize the datastructure with a list of `parents` for each node. The parents list will start with a base case if -1 for each node, to represent that each node is initially its own parent. Second, we will initialize an integer `num_independent` that starts at `n` and represents the count of unconnected nodes
* `find(nodeA)`: We will recursively call `find` on the parent of nodeA until we reach the base case where the parent is -1. Once we find the root node, we will perform a quick path compression technique, essentially caching the results so that it is `O(1)` on the next lookup. Finally, we will return the result
* `connect(inputA, inputB)` First, the problem states that nodes are  _"labeled from 1 to n"_. Essentially since we are keeping our parents array 0 indexed but the input labels are 1 indexed we must convert. Luckily, the tricky part is recognizing this. Once we recognize it it's just a matter of subtracting 1 from inputA and inputB in order to get nodeA and nodeB. Next, we will find the roots of nodeA and nodeB. If the two roots are not equal then this meens that a merge needs to happen. For a merge to happen:
    - We set the parent of one root to be the parent of the other root. 
    - We decrement our count of `num_independent` by 1
* `query`: The problem states that this function "Returns the number of connected component in the graph". This is easy since we are already keeping count! Just return `num_independent`

# Complexity

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
        self.parents[nodeA] = res # Necessary in order to avoid a Time Limit Exceeded
        return res

    def connect(self, inputA, inputB):
        nodeA = inputA - 1
        nodeB = inputB - 1

        rootA = self.find(nodeA)
        rootB = self.find(nodeB)

        if rootA != rootB:
            self.parents[rootA] = rootB 
            self.num_independent -= 1

    """
    @return: An integer
    """
    def query(self):
        return self.num_independent
 ```
