141. 环形链表
~~~java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null || head.next == null) {
            return false;
        }
        ListNode fast = head.next;
        ListNode slow = head;
        while (fast != slow) {
            if (fast.next == null || fast.next.next == null) {
                return false;
            }
            fast = fast.next.next;
            slow = slow.next;
        }
        return true;
    }
}
~~~


面试题47. 礼物的最大价值
~~~java
class Solution {
    public int maxValue(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        int[][] dp = new int[m+1][n+1];
        for(int i = 1; i <= m; i++) {
            for(int j = 1; j <= n; j++) {
                dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]) + grid[i-1][j-1];
            }
        }
        return dp[m][n];
    }
}
~~~

741. 摘樱桃
~~~java
class Solution {
    public int cherryPickup(int[][] grid) {
        int n = grid.length;
        int[][] dp = new int[n+1][n+1];
        for(int[] row : dp) {
            Arrays.fill(row, Integer.MIN_VALUE);
        }
        dp[n-1][n-1] = grid[n-1][n-1];
        for(int k = 2*(n-1)-1; k >= 0; k--) {
            for(int i1 = Math.max(0, k-n+1); i1 <= Math.min(n-1, k); i1++) {
                for(int i2 = i1; i2 <= Math.min(n-1, k); i2++) {
                    int j1 = k - i1;
                    int j2 = k - i2;
                    if (grid[i1][j1]==-1 || grid[i2][j2]==-1) {
                        dp[i1][i2] = Integer.MIN_VALUE;
                    } else {
                        if (i1 != i2 || j1 != j2) {
                            dp[i1][i2] = 
                                grid[i1][j1] + grid[i2][j2] + 
                                Math.max(
                                    Math.max(dp[i1][i2 + 1], dp[i1 + 1][i2]), 
                                    Math.max(dp[i1][i2], dp[i1 + 1][i2 + 1]));
                        } else {
                            dp[i1][i2] = grid[i1][j1] + 
                                Math.max(
                                    Math.max(dp[i1][i2 + 1], dp[i1 + 1][i2]), 
                                    Math.max(dp[i1][i2], dp[i1 + 1][i2 + 1]));
                        }
                    }
                }
            }
        }
        return Math.max(0, dp[0][0]);
    }
}
~~~
