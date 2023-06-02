# Strict or Inclusive Comparisons
Should I use `<`, `>`, or should I use `<=`, `>=`??? That is a tricky question. I found that to use minimal brain power (which is important during a high stress interview) you should always use `<` or `>` (strict approach) and then consider a separate case for `==`. In this way, you are being strict up front. In some cases the strict approach is indeed the answer. In other cases, being strict can cost you more lines of code but this is better than costing you the answer. Code can always be cleaned up later. 

Consider the following two examples

## Example 1: 
[Leetcode 704 - Binary Search](https://leetcode.com/problems/binary-search/description/)

Inclusive approach
```
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1
        while left <= right:
            mid = (left + right) // 2
            if nums[mid] == target:
                return mid
            if nums[mid] < target: # target must be in the right side
                left = mid + 1
            if nums[mid] > target: # target must be in the left side
                right = mid - 1
        return -1
```

Strict approach
```
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums) - 1
        while left < right:
            mid = (left + right) // 2
            if nums[mid] == target:
                return mid
            if nums[mid] < target: # target must be in the right side
                left = mid + 1
            if nums[mid] > target: # target must be in the left side
                right = mid - 1
        
        # One choice remaining
        if left == right:
            if nums[left] == target: 
                return left
            else:
                return -1

        # Invalid, thus not found
        if left > right:
            return -1
```


## Example 2:

[Leetcode 235 - Lowest Common Ancestor of a Binary Search Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)

Inclusive approach
Not even a viable answer.

Strict approach
```
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        cur = root
        while cur:

            # Both go to the left
            if p.val < cur.val and q.val < cur.val:
                cur = cur.left

            # Both go to the right
            elif p.val > cur.val and q.val > cur.val:
                cur = cur.right

            # We have a split.
            # p = cur
            # q = cur
            # < >
            # > < 
            else:
                return cur
```             
