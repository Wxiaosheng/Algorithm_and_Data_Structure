## 独一无二的出现次数

给你一个整数数组 arr，请你帮忙统计数组中每个数的出现次数。

如果每个数的出现次数都是独一无二的，就返回 true；否则返回 false。

    示例 1：
      输入：arr = [1,2,2,1,1,3]
      输出：true
      解释：在该数组中，1 出现了 3 次，2 出现了 2 次，3 只出现了 1 次。没有两个数的出现次数相同。

    示例 2：
      输入：arr = [1,2]
      输出：false

### 解法一： loop + map

```javascript
var uniqueOccurrences = function (arr) {
  const map = new Map()
  for (let n of arr) {
    const count = map.has(n) ? map.get(n) : 0
    map.set(n, count+1)
  }
  const hash = {}, values = map.values()
  for (let v of values) {
    if (hash[v] !== undefined) return false
    hash[v] = true
  }
  return true
}
```

### 解法二： 优化 数组判重
* 数组去重，array => set => array
* 数组判重，array => set => 判断元素个数是否变化

```javascript
var uniqueOccurrences = function () {
  const map = new Map()
  for (let n of arr) {
    const count = map.has(n) ? map.get(n) : 0
    map.set(n, count + 1)
  }
  return map.size === (new Set(map.values())).size
}
```