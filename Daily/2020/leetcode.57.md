## 插入区间
给出一个无重叠的 ，按照区间起始端点排序的区间列表。  
在列表中插入一个新的区间，你需要确保列表中的区间仍然有序且不重叠（如果有必要的话，可以合并区间）。

     示例 1：
      输入：intervals = [[1,3],[6,9]], newInterval = [2,5]
      输出：[[1,5],[6,9]]

    示例 2：
      输入：intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
      输出：[[1,2],[3,10],[12,16]]
      解释：这是因为新的区间 [4,8] 与 [3,5],[6,7],[8,10] 重叠。
  
#### 解法一： 记录所有区间，标记边界，最后汇总

```javascript
var insert = function (intervals, newInterval) {
  const result = [], map = new Map(), total = [...intervals, newInterval]
  for (let i = 0; i < total.length; i++) {
    let [left, right] = total[i]
    // 标记 [0, 0] 这种的区间
    if (left === right) map.set(left, map.get(left) || "self")
    while (left < right) {
      map.set(left++, true)
    }
    map.set(right, map.get(right))
  }
  let start, isRecor = false, hash = Array.from(map.entries()).sort((a, b) => a[0] - b[0])
  for (let i = 0; i < hash.length; i++) {
    const [key, value] = hash[i]
    if (isRecor) {
      if (!value || value == "self") result.push([start, key]), isRecor = false
    } else {
      if (value == "self") result.push([key, key])
      else if (value) start = key, isRecor = true
    }
  }
  return result
}
```

