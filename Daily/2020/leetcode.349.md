## LeetCode 349 两个数组的交集
给定两个数组，编写一个函数来计算它们的交集。

    示例 1：
      输入：nums1 = [1,2,2,1], nums2 = [2,2]
      输出：[2]

    示例 2：
      输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
      输出：[9,4]

说明：
* 输出结果中的每个元素一定是唯一的。
* 我们可以不考虑输出结果的顺序。


#### 解法一：Array API
**过滤 + 去重 + toArray**

```javascript
var intersection = function (nums1, nums2) {
  if (nums1.length == 0 || nums2.length == 0) return []
  return Array.from(new Set(nums1.filter(n => nums2.includes(n))))
}
```