# Union Find

https://www.geeksforgeeks.org/union-by-rank-and-path-compression-in-union-find-algorithm/

```
* Initialize
    * Such that each cell is an "orphan" with parent -1
    * The count is 0 (we will increment the count as part the main algorithm)
* `find(self, node)` 
    * Get the parent of `node`  
    * If `node` is an orphan (we are guaranteed at least one orphan)
        * Then return `node`. It is its own parent
    * Otherwise, recursively call `find` on the parent of `node`
```
