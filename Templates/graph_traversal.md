# Graph Traversal - BFS/DFS

First check the matrix traversal template [**HERE**](./matrix_traversal.md) if you haven't seen it. It is highly recommended that you fully understand the matrix traversal first.

We can use either BFS or DFS to traversal the graph

- Key Differences Between BFS and DFS
    1. BFS is vertex-based algorithm while DFS is an edge-based algorithm.
    2. Queue data structure is used in BFS. On the other hand, DFS uses stack or recursion.
    3. Memory space is efficiently utilized in DFS while space utilization in BFS is not effective.
        - DFS takes linear space because we have to remember single path with unexplored nodes, while BFS keeps every node in memory.
    4. BFS is optimal algorithm while DFS is not optimal.
    5. DFS constructs narrow and long trees. As against, BFS constructs wide and short tree.


## Recursive template

```python
def traverse(matrix):
    """Recursive"""
    
    rows, cols = len(matrix), len(matrix[0])
    visited = set()
    directions = ((0, 1), (0, -1), (1, 0), (-1, 0))  # Much faster than list

    def dfs(i, j):
        if (i, j) in visited:
            return
        visited.add((i, j))
        
        # Traverse neighbors
        for direction in directions:
            next_i, next_j = i + direction[0], j + direction[1]
            if 0 <= next_i < rows and 0 <= next_j < cols: # Check boundary
                # Add any other checking here ^
                dfs(next_i, next_j)
            
    for i in range(rows):
        for j in range(cols):
            dfs(i, j)
```

## Iterative template

```python
# BFS TEmplate for LC 200

def numIslands(self, grid: List[List[str]]) -> int:
    count = 0

    if not grid:
        return count

    rows = len(grid)
    cols = len(grid[0])
    directions = ((0, 1), (0, -1), (1, 0), (-1, 0))

    for row in range(rows):
        for col in range(cols):
            if grid[row][col] == '1':
                # The position here is critical
                # count here means counting all the "1"s
                count += 1
                grid[row][col] = 'visited' # Mark current node as visited
                queue = [(row, col)]  # Initiate a queue for bfs

                while queue:
                    for _ in range(len(queue)):
                        # Must use name other than row and col
                        # Otherwise there will be collision
                        _x, _y = queue.pop(0)

                        for dx, dy in directions:
                            # Traversal all directions
                            x, y = dx + _x, dy + _y

                            if 0 <= x < rows and 0 <= y < cols and grid[x][y] == "1":
                                grid[x][y] = 'visited'
                                queue.append((x, y))
                            
                            # if count is here (i.e. inside all loops) it'll count how many "1"s
                    
                    # If count is here, (i.e. out of the two for loops) 
                    # it'll count how many steps it'll need from the position 
                    # to go to all the other places (i.e. leetcode 994)

    return count
```

Reference:

- [Tips for all DFS in matrix question](https://leetcode.com/problems/pacific-atlantic-water-flow/discuss/90739/python-dfs-bests-85-tips-for-all-dfs-in-matrix-question)

Practice:

- [200. Number of Islands](https://leetcode.com/problems/number-of-islands/)
- [130. Surrounded Regions](https://leetcode.com/problems/surrounded-regions/)
- [695. Max Area of Island](https://leetcode.com/problems/max-area-of-island/)
- [994. Rotting Oranges](https://leetcode.com/problems/rotting-oranges/)

