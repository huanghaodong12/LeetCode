746. 使用最小花费爬楼梯
~~~java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int n = cost.length;
        for(int i = 2; i < n; i++) {
            cost[i] += Math.min(cost[i-1], cost[i-2]);
        }
        return Math.min(cost[n-1], cost[n-2]);
    }
}
~~~

718. 最长重复子数组
~~~java
class Solution {
    public int findLength(int[] A, int[] B) {
        int m = A.length;
        int n = B.length;
        int[][] dp = new int[m+1][n+1];
        int res = 0;
        for(int i = 1; i <= m; i++) {
            for(int j = 1; j <= n; j++) {
                if (A[i-1] == B[j-1]) {
                    dp[i][j] = dp[i-1][j-1] + 1;
                    res = Math.max(res, dp[i][j]);
                }
            }
        }
        return res;
    }
}
~~~

123. 买卖股票的最佳时机 III
~~~java
class Solution {
    public int maxProfit(int[] prices) {
        int n = prices.length;
        int[][] dp = new int[n+1][5];
        for(int i = 1; i <= n; i++) {
            for(int j = 0; j < 5; j++) {
                if (j%2==0) {
                    dp[i][j] = dp[i-1][j];
                    if (j > 0 && i > 1) {
                        dp[i][j] = Math.max(dp[i][j], dp[i-1][j-1]+prices[i-1]-prices[i-2]);
                    }
                } else {
                    dp[i][j] = dp[i-1][j-1];
                    if (i > 1) {
                        dp[i][j] = Math.max(dp[i][j], dp[i-1][j]+prices[i-1]-prices[i-2]);
                    }
                }
            }
        }
        return Math.max(dp[n][0], Math.max(dp[n][2], dp[n][4]));
    }
}
~~~
