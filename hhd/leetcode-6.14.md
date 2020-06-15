605. 种花问题
~~~java
class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        int count = 0;
        for(int i = 0; i < flowerbed.length; i++) {
            if (flowerbed[i] == 1) {
                count++;
            }
        }
        int[] dp = new int[flowerbed.length+2];
        for(int i = 2; i < dp.length; i++) {
            if (i+1 < dp.length && flowerbed[i-1]==1) {
                dp[i] = dp[i-1];
            } else {
                dp[i] = Math.max(dp[i-1], dp[i-2]+1);
            }
        }
        return dp[flowerbed.length+1]-count >= n;
    }
}
~~~

877. 石子游戏
~~~java
class Solution {
    public boolean stoneGame(int[] piles) {
        int n = piles.length;
        int[][] dp = new int[n][n];
        for(int len = 0; len < n; len++) {
            for(int i = 0; i < n-len; i++) {
                if (len == 0) {
                    dp[i][i] = piles[i];
                    continue;
                }
                int j = i+len;
                dp[i][j] = Math.max(piles[i]-dp[i+1][j], piles[j]-dp[i][j-1]);
            }
        }
        return dp[0][n-1]>0;
    }
}
~~~

1140. 石子游戏 II
~~~java
class Solution {
    
    int[][] memory;
    int[] sum;

    public int stoneGameII(int[] piles) {
        int n = piles.length;
        memory = new int[n+1][n+1];
        sum = new int[n+1];
        for(int i = 1; i <= n; i++) {
            sum[i] = sum[i-1] + piles[i-1];
        }

        return dfs(piles, 1, 1);
    }


    public int dfs(int[] piles, int i, int M) {
        if (memory[i][M] > 0) {
            return memory[i][M];
        }
        if (i > piles.length) {
            return 0;
        }
        if (i + 2*M > piles.length) {
            memory[i][M] = sum[piles.length] - sum[i-1];
            return memory[i][M];
        }
        int max = 0;
        for(int k = 1; k <= 2*M; k++) {
            int next = dfs(piles, i+k, Math.max(k, M));
            max = Math.max(max, sum[piles.length] - sum[i-1] - next);
        }
        memory[i][M] = max;
        return memory[i][M];
    }
   
}
~~~

1406. 石子游戏 III
~~~java
class Solution {
    int n;
    int[] dp;
    int[] memery;

    public String stoneGameIII(int[] stoneValue) {
        n = stoneValue.length;
        memery = new int[n+1];
        dp = new int[n+1];
        for(int i = 1; i <= n; i++) {
            dp[i] = dp[i-1] + stoneValue[i-1];
        }
        int res = 2*dfs(1);
        if (res == dp[n]) {
            return "Tie";
        } else if (res > dp[n]) {
            return "Alice";
        } else {
            return "Bob";
        }
    }

    public int dfs(int i) {
        if (i > n) {
            return 0;
        }
        if (memery[i] != 0) {
            return memery[i];
        }
        int min = Integer.MAX_VALUE;
        for(int k = 1; k <= 3; k++) {
            min = Math.min(min, dfs(i+k));
        }
        memery[i] = dp[n] - dp[i-1] - min;
        return memery[i];
    }
}
~~~
