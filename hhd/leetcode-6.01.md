面试题 16.17. 连续数列
~~~java
class Solution {
    public int maxSubArray(int[] nums) {
        int res = nums[0];
        for(int i = 1; i < nums.length; i++) {
            if (nums[i-1] > 0) {
                nums[i] += nums[i-1];
            }
            res = Math.max(res, nums[i]);
        }
        return res;
    }
}
~~~



1431. 拥有最多糖果的孩子
~~~java
class Solution {
    public List<Boolean> kidsWithCandies(int[] candies, int extraCandies) {
        int max = candies[0];
        for(int i = 1; i < candies.length; i++) {
            if (candies[i] > max) {
                max = candies[i];
            }
        }
        List<Boolean> list = new ArrayList<>();
        for(int i = 0; i < candies.length; i++) {
            if (candies[i]+extraCandies >= max) {
                list.add(true);
            } else {
                list.add(false);
            }
        }
        return list;
    }
}
~~~


206. 反转链表
~~~java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode res = new ListNode(0);
        while(head != null) {
            ListNode temp = head;
            head = head.next;
            temp.next = res.next;
            res.next = temp;
        }
        return res.next;
    }
}
~~~


877. 石子游戏
class Solution {
    public boolean stoneGame(int[] piles) {
        int n = piles.length;
        int[][] dp = new int[n][n];
        for(int len = 0; len < n; len++) {
            for(int i = 0; i < n-len; i++) {
                int j = i + len;
                if (i == j) {
                    dp[i][j] = piles[i];
                    continue;
                }
                dp[i][j] = Math.max(piles[i]-dp[i+1][j], piles[j]-dp[i][j-1]);
            }
        }
        return dp[0][n-1]>0;
    }
}


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



1320. 二指输入的的最小距离
~~~java
class Solution {
    public int minimumDistance(String word) {
        int n = word.length();
        int[][][] dp = new int[n+1][26][26];
        for(int i = 1; i <= n; i++) {
            for(int j = 0; j < 26; j++) {
                Arrays.fill(dp[i][j], Integer.MAX_VALUE);
            }
        }
        int res = Integer.MAX_VALUE;
        for(int i = 1; i <= n; i++) {
            int val = word.charAt(i - 1) - 'A';
            for(int l = 0; l < 26; l++) {
                for(int r = 0; r < 26; r++) {
                    if (dp[i-1][l][r] != Integer.MAX_VALUE) {
                        dp[i][val][r] = Math.min(dp[i][val][r], dp[i-1][l][r]+getLength(val, l));
                        dp[i][l][val] = Math.min(dp[i][l][val], dp[i-1][l][r]+getLength(val, r));
                    }
                    if (i == n) {
                        res = Math.min(res, Math.min(dp[i][l][val], dp[i][val][r]));
                    }
                }
            }
        }
        return res;
    }


    public int getLength(int  i1, int i2) {
        return Math.abs(i1/6-i2/6) + Math.abs(i1%6-i2%6);
    }

}
~~~
