**Beta:** Not linked to anything.
# List of optimization techniques

## Redundancy Optimization
If you are redunantly counting then try using a frequency count instead

Problems:
- https://leetcode.com/problems/number-of-good-ways-to-split-a-string/solutions/3075325/redundancy-optimization/

## Count as you go
Suppose that the core to a problem is to do some N operations and then count how many times a particular element occurs. Rather than looping through a list of N, we can keep a count as we go through the N operations the first time.

More specificlly, we can either manage the count by starting at 0 and counting up, or by starting at N and counting down.

Problems: 
- https://github.com/tjm165/algorithms-practice/blob/main/additional-explanations/alternative-problems/leetcode-323.md
