## 求根到叶子节点数字之和

给定一个二叉树，它的每个结点都存放一个 0-9 的数字，每条从根到叶子节点的路径都代表一个数字。

例如，从根到叶子节点路径 1->2->3 代表数字 123。

计算从根到叶子节点生成的所有数字之和。

说明: 叶子节点是指没有子节点的节点。

    示例 1:
      输入: [1,2,3]
              1
             / \
            2   3
      输出: 25
      解释:
        从根到叶子节点路径 1->2 代表数字 12.
        从根到叶子节点路径 1->3 代表数字 13.
        因此，数字总和 = 12 + 13 = 25.

    示例 2:
      输入: [4,9,0,5,1]
                4
               / \
              9   0
             / \
            5   1
      输出: 1026
      解释:
        从根到叶子节点路径 4->9->5 代表数字 495.
        从根到叶子节点路径 4->9->1 代表数字 491.
        从根到叶子节点路径 4->0 代表数字 40.
        因此，数字总和 = 495 + 491 + 40 = 1026.


#### 解法一： DFS - 深度优先搜索
* 自己想出来的题解

```javascript
var sumNumbers = function (root) {
  if (root == null) return 0
  let sum = 0
  const helper = function (node, sub) {
    // terminatro
    if (node.left == null && node.right == null) {
      sub.push(node.val)
      return sum += Number(join(''))
    }
    // process current logic
    if (node.left) helper(node.left, [...sub, node.val])
    if (node.right) helper(node.right, [...sub, node.val])
    // dirll down
    // restore
  }

  helper(root, [])
  return sum
}
```

**缺点： 空间复杂度是 O(n)，可以优化为 O(1)**

```javascript
var sumNumbers = function (root) {
  if (root == null) return 0
  let sum = 0
  const helper = function (node, sub) {
    if (node.left == null && node.right == null) {
      return sum += sub * 10 + node.val
    }
    if (node.left) helper(node.left, sub*10 + node.val)
    if (node.right) helper(node.right, sub*10 + node.val)
  }
  helper(root, 0)
  return sum
}
```

#### 解法二： DFS - 广度优先搜索
另一种 DFS 的递归方式

```javascript
var sumNumbers = function (root) {
  if (root == null) return 0
  const dfs = function (node, preSum) {
    const sum = preSum * 10 + node.val
    if (node.left == null && node.right == null) return sum
    return dfs(node.left, sum) + dfs(node.right, sum)
  }
  return dfs(root, 0)
}
```

#### 解法三： BFS - 广度优先搜索
思路：一层一层的扩散，并且下一层会记录从根结点到当前一层的累计

```javascript
var sumNumbers = function (root) {
  if (root == null) return 0
  let sum = 0, queue = [[root, 0]]
  while (queue.length) {
    const [node, preSum] = queue.shift()
    const nextSum = preSum * 10 + node.val
    if (node.left == null && node.right == null) {
      sum += nextSum
    }
    if (node.left) queue.push([node.left, nextSum])
    if (node.right) queue.push([node.right, nextSum])
  }
  return sum
}
```
