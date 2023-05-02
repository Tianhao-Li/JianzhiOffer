# 剑指 Offer 16. 数值的整数次方

## Description

实现 pow(x, n) ，即计算 x 的 n 次幂函数（即，$x^n$）。不得使用库函数，同时不需要考虑大数问题。

 

示例 1：

输入：x = 2.00000, n = 10
输出：1024.00000
示例 2：

输入：x = 2.10000, n = 3
输出：9.26100
示例 3：

输入：x = 2.00000, n = -2
输出：0.25000
解释：2-2 = 1/22 = 1/4 = 0.25


提示：

-100.0 < x < 100.0
-2^31 <= n <= 2^31-1
-10^4 <= $x^n$ <= 10^4



## Solution

> Recursion + some conversion of the problem

- Convert the cases where n is negative to positive
- Note the range of n, this solution requires us to use long

```java
class Solution {
    public double myPow(double x, int n) {
        // Recursion + optimization of calculating half
        long N = n;

        if (N < 0) {
            x = 1 / x;
            N = -N;
        }

        return fastPow(x, N);
    }

    private double fastPow(double x, long n) {
        // Base case
        if (n == 0) {
            return 1;
        } else if (x == 0) {
            return 0;
        } else if (n == -1) {
            return 1/x;
        }

        // Recursive call
        double half = fastPow(x, n / 2);

        // Operation at current
        if (n % 2 == 0) {
            return half * half;
        } else {
            return half * half * x;
        }
    }
}
```



- TC: O(log n)
- SC: O(log n)