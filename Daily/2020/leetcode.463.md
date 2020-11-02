## 岛屿的周长

给定一个包含 0 和 1 的二维网格地图，其中 1 表示陆地 0 表示水域。

网格中的格子水平和垂直方向相连（对角线方向不相连）。整个网格被水完全包围，但其中恰好有一个岛屿（或者说，一个或多个表示陆地的格子相连组成的岛屿）。

岛屿中没有“湖”（“湖” 指水域在岛屿内部且不和岛屿周围的水相连）。格子是边长为 1 的正方形。网格为长方形，且宽度和高度均不超过 100 。计算这个岛屿的周长。

    示例：
      输入:
        [
          [0,1,0,0],
          [1,1,1,0],
          [0,1,0,0],
          [1,1,0,0]
        ]

      输出: 16
      解释: 它的周长是下面图片中的 16 个黄色的边

### 解法一： loop
遍历整个地图，当遇见岛屿时，初始化 4 条边，如果 上下左右 四个方向上有相邻的岛屿，则减少一条边
```javascript
var islandPerimeter = function (grid) {
  if (grid.length == 0) return 0
  let result = 0
  const m = grid.length, n = grid[0].length
  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      if (grid[i][j] == 0) continue
      result += 4
      if (i - 1 > -1 && grid[i - 1][j] == 1) result--
      if (i + 1 < m && grid[i + 1][j] == 1) result--
      if (j - 1 > -1 && grid[i][j - 1] == 1) result--
      if (j + 1 < n && grid[i][j + 1] == 1) result--
    }
  }
  return result
}
```

### 解法二： DFS - 深度优先搜索

```javascript
var islandPerimeter = function (grid) {
 
}
```