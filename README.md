# Data Structures and Algorithms in Python
1. [Arrays and Strings](#arr)
2. [Matrices](#matrix)
3. [Linked Lists](#ll)
4. [Stacks and Queues](#stacks)
4. [Trees](#trees)
5. [Graphs](#graphs)

## Arrays and Strings <a name="arr"></a>
Some introduction text, formatted in heading 2 style

## Matrices <a name="matrix"></a>
### Modifying a matrix in-place
- Rotation
### Matrix traversals
- Linear
- Diagonal
- Spiral
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

## Linked Lists <a name="ll"></a>
This is a sub paragraph, formatted in heading 3 style

## Stacks and Queues <a name="stacks"></a>
The second paragraph text

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

Maximum Width of a Binary Tree at depth (or height) h can be 2h where h starts from 0 - perfect Binary Tree.
Height for a Balanced Binary Tree is O(Log n). Worst case occurs for skewed tree and worst case height becomes O(n).

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
The second paragraph text
