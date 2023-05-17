###解题思路

最简单无脑的当然就是用递归回溯做了，但是时间复杂度上会高很多，而且n比较大的情况下，递归多了容易StackOverFlow


### 动态规划的做法:

首先声明定义DP为一维数组，数组的下标值代表了f(n)中的n，数组的值存储的是自变量n对应的函数值

DP的递推公式也就是DP[i]=DP[i-1]=DP[i-2];

```java
public int fib(int n) {
     long[] dp = new long[101];
        dp[0] = 0L;
        dp[1] = 1L;
        int i;
        if (n < 2) {
            return n;
        }
        for (i = 2; i <= n; i++) {
            dp[i] = (dp[i - 1] + dp[i - 2])%1000000007L;
        }
        return (int)dp[i - 1] ;
    }

```    