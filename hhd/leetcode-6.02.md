121. 买卖股票的最佳时机
~~~java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length <= 1) {
            return 0;
        }
        int res = 0;
        int preMax = prices[0];
        for(int i = 1; i < prices.length; i++) {
            res = Math.max(res, prices[i]-preMax);
            if (prices[i] < preMax) {
                preMax = prices[i];
            }
        }

        return res;
    }
}
~~~


122. 买卖股票的最佳时机 II
~~~java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length <= 1) {
            return 0;
        }
        int res = 0;
        for(int i = 1; i < prices.length; i++) {
            if (prices[i] > prices[i-1]) {
                res += prices[i] - prices[i-1];
            }
        }
        return res;
    }
}
~~~



547. 朋友圈
~~~java
class Solution {
    public int findCircleNum(int[][] M) {
        int n = M.length;
        boolean[] visited = new boolean[n];
        int count = 0;
        for(int i = 0; i < n; i++) {
            if (!visited[i]) {
                visited[i] = true;
                dfs(visited, M, i);
                count++;
            }
        }
        return count;
    }

    public void dfs(boolean[] visited, int[][]M, int i) {
        for(int j = 0; j < visited.length; j++) {
            if (M[i][j]==1 && !visited[j]) {
                visited[j] = true;
                dfs(visited, M, j);
            }
        }
    }
}
~~~


765. 情侣牵手
~~~java
class Solution {
    public int minSwapsCouples(int[] row) {
        int res = 0;
        for(int i = 0; i < row.length; i+=2) {
            int p1 = row[i];
            int p2 = (row[i]%2==0?row[i]+1:row[i]-1);
            if (row[i+1] != p2) {
                for(int j = i+2; j < row.length; j++) {
                    if (row[j] == p2) {
                        row[j] = row[i+1];
                        row[i+1] = p2;
                        break;
                    }
                }
                res++;
            }
        }

        return res;
    }
}
~~~
