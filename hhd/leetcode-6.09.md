1046. 最后一块石头的重量
~~~java
class Solution {
    public int lastStoneWeight(int[] stones) {
        int n = stones.length;
        if (n == 1) {
            return stones[0];
        }
        int max1 = -1;
        int max2 = -1;
        for(int len = 1; len < n; len++) {
            for(int i = 0; i < n; i++) {
                if (stones[i] == 0 || max2 == i) {
                    continue;
                }
                if (max2==-1 || stones[i] > stones[max2]) {
                    max1 = max2;
                    max2 = i;
                } else if (max1==-1 || stones[i] > stones[max1]) {
                    max1 = i;
                }
            }
            System.out.println(max2 + " : "  + max1);
            stones[max2] = stones[max2] - stones[max1];
            stones[max1] = 0;
        }
        return stones[max2];
    }
}
~~~


973. 最接近原点的 K 个点
~~~java
class Solution {
    public int[][] kClosest(int[][] points, int K) {
        int[][] res = new int[K][2];
        for(int i = 0; i < K; i++) {
            res[i][0] = 10001;
            res[i][1] = 10001;
        }
        int n = points.length;
        for(int i = 0; i < n; i++) {
            int curSqrt = points[i][0]*points[i][0] + points[i][1]*points[i][1];
            int j = 0;
            int sqrt = res[j][0]*res[j][0] + res[j][1]*res[j][1];
            if (sqrt > curSqrt) {
                j = 1;
                while(j < K) {
                    sqrt = res[j][0]*res[j][0] + res[j][1]*res[j][1];
                    if (sqrt <= curSqrt) {
                        break;
                    }
                    res[j-1][0] = res[j][0];
                    res[j-1][1] = res[j][1];
                    j++;
                }
                res[j-1][0] = points[i][0];
                res[j-1][1] = points[i][1];
            }
        }
        return res;
    }
}
~~~


面试题46. 把数字翻译成字符串
~~~java
class Solution {
    public int translateNum(int num) {
        String str = String.valueOf(num);
        int n = str.length();
        int[] dp = new int[n+1];
        dp[0] = 1;
        dp[1] = 1;
        for(int i = 2; i <= n; i++) {
            dp[i] = dp[i-1];
            if (str.charAt(i-2)!='0' && Integer.parseInt(str.substring(i-2, i)) <= 25) {
                dp[i] += dp[i-2];
            }
        }
        return dp[n];
    }
}
~~~


778. 水位上升的泳池中游泳
~~~java
class Solution {
    public int swimInWater(int[][] grid) {
        int n = grid.length;
        boolean[][] dp = new boolean[n][n];
        PriorityQueue<Integer> queue = new PriorityQueue<>((i1, i2) -> {
            return grid[i1/n][i1%n] - grid[i2/n][i2%n];
        });
        queue.offer(0);
        dp[0][0] = true;
        int res = 0;
        while(!queue.isEmpty()) {
            int m = queue.poll();
            int i = m/n;
            int j = m%n;
            res = Math.max(res, grid[i][j]);
            if (i+1==n-1 && j==n-1 || i==n-1 && j+1==n) {
                break;
            }
            if (i+1 < n && !dp[i+1][j]) {
                queue.offer(m+n);
                dp[i+1][j] = true;
            }
            if (i-1 >= 0 && !dp[i-1][j]) {
                queue.offer(m-n);
                dp[i-1][j] = true;
            }
            if (j+1 < n && !dp[i][j+1]) {
                queue.offer(m+1);
                dp[i][j+1] = true;
            }
            if (j-1 >= 0 && !dp[i][j-1]) {
                queue.offer(m-1);
                dp[i][j-1] = true;
            }
        }
        return Math.max(res, grid[n-1][n-1]);
    }
}
~~~
