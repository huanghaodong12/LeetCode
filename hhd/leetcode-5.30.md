1025. 除数博弈
~~~java
class Solution {
    public boolean divisorGame(int N) {
        boolean[] dp = new boolean[N+1];
        dp[0] = true;
        for(int i = 1; i <= N; i++) {
            for(int j = 1; j <= i; j++) {
                if (i%j==0 && !dp[i-j]) {
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[N];
    }
}
~~~

764. 最大加号标志
~~~java
class Solution {
    public int orderOfLargestPlusSign(int N, int[][] mines) {
        int res = 0;
        int[][] dp1 = new int[N][N];
        int[][] dp2 = new int[N][N];
        for(int i = 0; i < N; i++) {
            for(int j = 0; j < N; j++) {
                dp1[i][j] = 1;
                dp2[i][j] = 1;
            }
        }
        for(int i = 0; i < mines.length; i++) {
            dp1[mines[i][0]][mines[i][1]] = 0;
            dp2[mines[i][0]][mines[i][1]] = 0;
        }
        for(int i = 0; i < N; i++) {
            for(int j = 0; j < N; j++) {
                if (dp1[i][j] == 1) {
                    res = 1;
                }
                if (j>0 && dp1[i][j] == 1) {
                    dp1[i][j] = dp1[i][j-1] + 1;
                }
                if (i>0 && dp2[i][j] == 1) {
                    dp2[i][j] = dp2[i-1][j] + 1;
                }
            }
        }
        for(int i = 1; i < N-1; i++) {
            for(int j = 1; j < N-1; j++) {
                if (dp1[i][j] != 0) {
                    int len = Math.min(dp1[i][j-1], dp2[i-1][j]);
                    for(int k = len; k >= 1; k--) {
                        if (j+k<N&&dp1[i][j+k]>=k&&i+k<N&&dp2[i+k][j]>=k) {
                            res = Math.max(res, k+1);
                            break;
                        }
                    }
                }
            }
        }
        return res;
    }
}
~~~


面试题 17.24. 最大子矩阵
~~~java
class Solution {
    public int[] getMaxMatrix(int[][] matrix) {
        int[] res = new int[4];
        int M = matrix.length;
        int N = matrix[0].length;
        int[] dp = new int[N];
        int beginR = 0;
        int beginC = 0;
        int count = 0;
        int sum = Integer.MIN_VALUE;
        for(int i = 0; i < M; i++) {
            for(int j = i; j < M; j++) {
                count = 0;
                for(int k = 0; k < N; k++) {
                    dp[k] += matrix[j][k];
                    if (count > 0) {
                        count += dp[k];
                    } else {
                        count = dp[k];
                        beginR = i;
                        beginC = k;
                    }
                    if (count > sum) {
                        sum = count;
                        res[0] = beginR;
                        res[1] = beginC;
                        res[2] = j;
                        res[3] = k;
                    }

                }
                
            }
            for(int k = 0; k < N; k++) {
                dp[k] = 0;
            }
        }
        return res;
    }
}
~~~
