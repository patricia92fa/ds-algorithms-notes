# Data Structures and Algorithms in Python
1. [Arrays and Strings](#arr)
2. [Matrices](#matrix)
3. [Linked Lists](#ll)
4. [Stacks and Queues](#stacks)
4. [Trees](#trees)
5. [Graphs](#graphs)
6. [Backtracking](#back)
7. [Combinatory 101](#comb)

## Arrays and Strings <a name="arr"></a>
An array is a **random access** data structure where each element can be accessed in `O(1)`. Random access is critical to many algorithms, i.e. binary search.
### Basic String manipulation
- `text.split($separator, $num_splits)`
- `str.maketrans($from, $to)`: creates a translation table. It is applied to using `text.translate(table)`, which iterates in text and substitutes all characters in `$from` to `$to` and leave the rest as is.
- `text.find(seq, start, end)`: returns the lowest idx in `text` where the sequence `seq` is found such that it is fully contained in `s[start:end]`. Returns `-1` on failure.
- `string.count(seq, start, end)`: returns the number of non-overlapping occurrences of substring `seq` in string `s[start:end]`. 
- `string.strip(s, char)`: returns a copy of the string with *only* leading and trailing characters removed. If you need to remove all chars in any position, use split with the to-be-deleted char as a separator, the join the result.
Remember **strings are immutable**. Therefore, any changes must be reassigned to the original variable.

### Custom Sort key
```python
def id_type(arr):
    _id, data = arr.split(" ", 1)
    return (0, data, _id) if data[0].isalpha() else (1, )
return sorted(logs, key = id_type)
```

#### Two pointers
#### Window

## Matrices <a name="matrix"></a>
### Modifying a matrix in-place
#### Rotation
#### Changing state
Some problems require identifying cells in a certain **state** and update the whole matrix at once according to certain rules (e.g. Game of life, Zero matrix). The key is to **mark** the cells to be updated by **encoding the previous and next status** and updating only the required positions as once. Therefore:
1. Iterate through the matrix and - after checking that you're within range - mark any state change accordingly:
```python
for r in range(rows):
    for c in range(cols):
        live_neighbours = 0
        for d in dirs:
            #### DO NOT MODIFY THE ITERATOR ####
            n_row, n_col = r + d[0], c + d[1]
            if 0 <= n_row < rows and 0 <= n_col < cols and (board[n_row][n_col] in [-1, 1]):
                live_neighbours += 1
        if board[r][c] == 1 and live_neighbours not in [2, 3]: board[r][c] = -1
        elif board[r][c] == 0 and live_neighbours == 3: board[r][c] = 2  
```
Be careful: when exploring neighbours use a different variable to access the cell e.g. `n_row`. **DO NOT MODIFY THE ITERATOR.**

2. Iterate again and update cells to their final value.

Note that for very large, sparse matrices, where the matrix may not even fit in memory. 
This way we can finally update the cell's value in a second matrix iteration, but still use the original value to compute any status updates in adjacent cells without using additional space.
### Matrix traversals
#### Linear
#### Diagonal
#### Spiral
A clean way to work with spiral traversals is to treat the matrix as layers.
While traversing, use explicit variables and ranges in order to avoid errors. For example, to traverse the last layer of a `nxn` matrix, we define layers to be of size `n - 1` so that they can be peeled individually with the same code - only changing boundaries. We peel the first row itertating through columns in `range(left, right)`. We proceed to peel the right-most layer, iterating through rows in `range(top, down)`. Similarly, when peeling from down to top in the first column, we iterate the reserved range:
```python
for i in reversed(range(top, down + 1)):
    matrix[i][left] = val
    val += 1
left += 1
```

### DP classic problems
#### Finding maximum subarea e.g. squares or rectangles
1. Init DP matrix with base cases
```python
dp = [[0 if matrix[r][c] == '0' else 1 for c in range(cols)] for r in range(rows)]
```
2. Linearly iterate matrix and cumulative sum size
```python
if matrix[r][c] == '1':
  dp[r][c] = min(dp[r - 1][c], dp[r][c - 1], dp[r - 1][c - 1]) + 1
```
The idea is that, when exploring linearly, for a cell to be the upper-right corner of a square the previously visited adjacent cells (i.e. upper, left and diagonal) must be also part of the same square. This translates to the min of their value plus the size (1) of the current cell.

#### Exploring all paths from cell
1. Iterate through the matrix and trigger DFS/BFS at appropriate cells
2. A clean way to explore all directions in each step is to iterate through **a list of direction tuples**:
```python
dirs = [(0, 1), (1, 0), (0, -1), (-1, 0)]
for d in dirs:
    dr, dc = r + d[0], c + d[1]
```
Make sure to check you're within range and that all conditions for valid paths still hold before advancing:
```python
if (0 <= dr < rows and 0 <= dc < cols and matrix[dr][dc] > matrix[r][c]):
  path_len = max(path_len, dfs(matrix, dr, dc))
```

## Linked Lists <a name="ll"></a>
A Linked List is a **sequential access** data structure, where each element can be accesed only in particular order.
Since the only access point to a Linked List is the `head` node, worst case TC for all operations is `O(n)`, as the desired element/position may be the last one and a traversal through all nodes is unavoidable.

### Common methods
- Insert and delete
- Find size
- Find middle node
### Common techniques
- Fast and slow pointers
- Sentinel/Dummy head: an invariant that it is always pointing to the current correct head.
### Reversal

## Stacks and Queues <a name="stacks"></a>
In general, stacks are used in matching/parsing problems, while queues are useful for preserving order i.e. in a cache implementation or an online metric computation.
### Iterative trees traversals
### Pair matching
### Circular queues

## Trees <a name="trees"></a>
### Concepts
- Height-balance means that at each step one has to pick up the number in the middle as a root.

- Given a sorted array of values, we can create a BST by recursively choosing the mid value:
[1, 2, 3, 4, 5, 6, 7] -> left: [1, 2, 3], root: 4, right: [5, 6, 7]
[1, 2, 3] -> left: [1], root: 2, right: [3]
[5, 6, 7] -> left: [5], root: 6, right: [7]
- Serialization
### Complexity
|       | DFS  | BFS  |
|-------|------|------|
| Time  | O(n) | O(n) |
| Space | O(h) | O(w) |

Maximum Width of a Binary Tree at depth (or height) `h` can be `2h` where `h` starts from `0` - perfect Binary Tree.
Height for a Balanced Binary Tree is `O(Log n)`. Worst case occurs for skewed tree and worst case height becomes `O(n)`.

### Usage
#### Modifying BT structure
#### Checking BT properties
- Top-down: maximum depth
- Botton-up: 
#### Generating a BT/BST
Given a sorted sequence `1 ... n`, to construct a BST, we can enumerate each number `i` in the sequence and use it as the root, then, the subsequence `1 ... (i-1)` on its left side would lay on the left branch of the root, and similarly the right subsequence `(i+1) ... n` lay on the right branch of the root. 

- Number of unique BSTs: DP

#### Adding new methods
- Implement Tree iterator

### Techniques
- Use tuples to solve traversal problems iteratively: 
```python
    def maxDepth(self, root: TreeNode) -> int:
        max_depth, nodes = 0, [(root, 0)]
        while nodes:
            node, level = nodes.pop()
            # GLOBAL MAX CAN BE UPDATED ONLY AT EACH LEAF
            if not node:
                max_depth = max(max_depth, level)
            else:
                nodes.append((node.right, level + 1))
                nodes.append((node.left, level + 1))
        return max_depth
```
Remember tuples are **not mutable**, so convert them to list if you need to alter them. However, their attributes **can** be altered!
## Graphs <a name="graphs"></a>
### Building adjacency lists
Given an egde list, building a graph is straightforward:
```python
        graph = {i:[] for i in range(num_nodes)}
        for v1, v2 in edges:
            graph[v1].append(v2)
            graph[v2].append(v1)
```
### Topological sort
A topological ordering of a graph is a linear ordering of all nodes where direction of the edges is maintained. 
- The graph must be **acyclic**, as this would prevent a linear ordering.
- All DAGs have a topological order which can be computed in `O(1)` time.
Simply build the graph taking into account the relationships between items. A common example is the ordering of taks i.e. one is a prerequisite of another. Then, traverse it using any traversal technique like BFS or DFS. Be mindful of where the traversal starts/stops and modify the result array if needed - e.g. DFS explores leaves first so you may need to reverse the result array.

## Backtracking <a name="back"></a>
The runtime of backtracking algorithms is `O(b^d)`, where `b` is the branching factor and `d` is the maximum depth of recursion. Backtracking is characterized by a number of decisions `b` that can be made at each level of recursion. If you visualize the recursion tree, this is the number of children each internal node has.

## Combinatory 101 <a name="comb"></a>
### Number of ways to partition a N elements into K subsets
A Stirling number of the second kind counts the number of ways to partition a set of `n` objects into `k` non-empty subsets.
We have `n + k - 1` places for dividors and elements, and `k - 1` divisors to choose from. So there are `C(n + k - 1, k - 1)` possibilities i.e. 
