# 剑指 Offer 04. 二维数组中的查找

## Description

在一个 n * m 的二维数组中，每一行都按照从左到右 非递减 的顺序排序，每一列都按照从上到下 非递减 的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

 

示例:

现有矩阵 matrix 如下：

[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
给定 target = 5，返回 true。

给定 target = 20，返回 false。

 

限制：

0 <= n <= 1000

0 <= m <= 1000



## Solution

> Similar to DP, Search Space Reduction

- 从左下角（或者右上角）开始搜索，根据大小关系可以确定向右还是向上搜索

```java
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        // Search from bottom-left corner, go right or go up
        int i = matrix.length - 1;
        int j = 0;

        while (i >= 0 && j < matrix[0].length) {
            int cur = matrix[i][j];

            if (matrix[i][j] == target) {
                return true;
            } else if (cur > target) {
                i--;
            } else {
                // cur < target
                j++;
            }
        }

        return false;
    }
}
```

- **TC: O(m + n)**
- **SC: O(1)**