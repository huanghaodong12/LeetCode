面试题10- I. 斐波那契数列
~~~java
class Solution {
    public int fib(int n) {
        if (n <= 0) {
            return 0;
        }
        if (n <= 2) {
            return 1;
        }
        int MOD = 1000000007;
        int num1 = 1;
        int num2 = 1;
        for(int i = 3; i <= n; i++) {
            int temp = num2;
            num2 = (num2+num1)%MOD;
            num1 = temp;
        }
        return num2;
    }
}
~~~

1143. 最长公共子序列
~~~java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int m = text1.length();
        int n = text2.length();
        int[][] dp = new int[n+1][m+1];
        for(int i = 1; i <= n; i++) {
            for(int j = 1; j <= m; j++) {
                if (text2.charAt(i-1) == text1.charAt(j-1)) {
                    dp[i][j] = dp[i-1][j-1] + 1;
                }
                dp[i][j] = Math.max(dp[i][j], dp[i][j-1]);
                dp[i][j] = Math.max(dp[i][j], dp[i-1][j]);
            }
        }
        return dp[n][m];
    }
}
~~~

1420. 生成数组
~~~java
class Solution {
    public int numOfArrays(int n, int m, int k) {
        if (n < k || m < k) {
            return 0;
        }
        int MOD = 1000000007;
        long[][][] dp = new long[n+1][k+1][m+1];
        for(int i = 1; i <= n; i++) {
            for(int j = 1; j <= k; j++) {
                for(int h = 1; h <= m; h++) {
                    if (i==1 && i==j) {
                        dp[i][j][h] = 1;
                        continue;
                    }
                    dp[i][j][h] = (dp[i-1][j][h] * h) % MOD;
                    for(int x = 1; x < h; x++) {
                        dp[i][j][h] = (dp[i][j][h]+dp[i-1][j-1][x]) % MOD;
                    }
                }
            }
        }
        for(int i = 1; i <= m; i++) {
            dp[n][k][i] = (dp[n][k][i] + dp[n][k][i-1]) % MOD;
        }
        return (int)dp[n][k][m];
    }
}
~~~
