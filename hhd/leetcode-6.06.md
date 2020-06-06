面试题 08.01. 三步问题
~~~java
class Solution {
    public int waysToStep(int n) {
        if (n <= 2) {
            return n;
        }
        if (n == 3) {
            return 4;
        }
        long MOD = 1000000007;
        long n1 = 1;
        long n2 = 2;
        long n3 = 4;
        for(int i = 4; i <= n; i++) {
            long temp3 = n3;
            long temp2 = n2;
            n3 = (n3 + n2 + n1)%MOD;
            n2 = temp3;
            n1 = temp2;
        }
        return (int)n3;
    }
}
~~~

面试题 08.02. 迷路的机器人
~~~java
class Solution {
    public List<List<Integer>> pathWithObstacles(int[][] obstacleGrid) {
        if (obstacleGrid==null || obstacleGrid.length<=0 || obstacleGrid[0].length<=0) {
            return new ArrayList<>();
        }
        this.obstacleGrid = obstacleGrid;
        m = obstacleGrid.length;
        n = obstacleGrid[0].length;
        visited = new boolean[m][n];
        flag = false;
        list = new LinkedList<>();
        rec(0, 0);
        return list;
    }

     int[][] obstacleGrid;
     boolean[][] visited;
     int m;
     int n;
     boolean flag = true;
     LinkedList<List<Integer>> list;

    public void rec(int i, int j) {
        if (i >= m || j >= n || obstacleGrid[i][j] == 1 || visited[i][j]) {
            return;
        }
        
        visited[i][j] = true;
        ArrayList<Integer> arrayList = new ArrayList<>(2);
        arrayList.add(i);
        arrayList.add(j);
        list.addLast(arrayList);

        if (i+1 == m && j+1 == n) {
            return;
        }

        rec(i, j+1);
        if (visited[m-1][n-1]) {
            return;
        }
        rec(i+1, j);    
        if (visited[m-1][n-1]) {
            return;    
        }
        list.removeLast();
    }
}
~~~


188. 买卖股票的最佳时机 IV
~~~java
class Solution {
    public int maxProfit(int k, int[] prices) {
        int n = prices.length;
        int sum = 0;        
        if (k >= n) {
            for(int i = 1; i < n; i++) {
                if (prices[i] - prices[i-1] > 0) {
                    sum += prices[i] - prices[i-1];
                }
            }
            return sum;
        }
        int[][] dp = new int[n+1][2*k+1];
        for(int i = 1; i <= n; i++) {
            for(int j = 0; j < 2*k+1; j++) {
                if (j % 2 == 0) {
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
        for(int i = 0; i < 2*k+1; i+=2) {
            sum = Math.max(sum, dp[n][i]);
        }
        return sum;
    }
}
~~~


128. 最长连续序列
~~~java
class Solution {
    public int longestConsecutive(int[] nums) {
        int len = 0;
        Set<Integer> set = new HashSet<>();
        for(int i = 0; i < nums.length; i++) {
            set.add(nums[i]);
        }
        for(int i = 0; i < nums.length; i++) {
            if (set.contains(nums[i] - 1)) {
                continue;
            }
            int value = nums[i]+1;
            while(set.contains(value)) {
                value++;
            }
            len = Math.max(len, value-nums[i]);
        }
        return len;
    }
}
~~~
