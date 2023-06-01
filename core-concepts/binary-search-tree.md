# Binary Search Tree
In a binary search tree every left node is less that the root. Every right node is greater than the root. 

## Advantages
- Be smarter about dfs. 

# Binary Search
Take advantage of data structures that have similar properties to a Binary Search Tree. This most commonly applies to a Binary Search Tree OR a sorted array

## Sample code for sorted array. 
See [Leetcode 704](https://leetcode.com/problems/binary-search/)
```
def binarySearch(self, nums: List[int], target: int) -> int:
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
