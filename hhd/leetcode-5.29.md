392. 判断子序列
~~~java
class Solution {
    public boolean isSubsequence(String s, String t) {
        if (t == null) {
            return false;
        }
        if (s == null) {
            return true;
        }
        if (s.length() > t.length()) {
            return false;
        }
        if (s.length() <= 0) {
            return true;
        }
        for(int i = 0, j = 0; i < t.length(); i++) {
            if (s.charAt(j) == t.charAt(i)) {
                j++;
            }
            if (j == s.length()) {
                return true;
            }
        }
        return false;
    }
}
~~~



1139. 最大的以 1 为边界的正方形
~~~java
class Solution {

    public int largest1BorderedSquare(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        int[][] dp1 = new int[m+1][n+1];
        int[][] dp2 = new int[m+1][n+1];
        int res = 0;
        for(int i = 1; i <= m; i++) {
            for(int j = 1; j <= n; j++) {
                if (grid[i-1][j-1] == 1) {
                    dp1[i][j] = dp1[i][j-1] + 1;
                    dp2[i][j] = dp2[i-1][j] + 1;
                    res = 1;
                }
            }
        }
        
        for(int i = 2; i <= m; i++) {
            for(int j = 2; j <= n; j++) {
                if (grid[i-1][j-1]==0||dp1[i][j-1]==0||dp2[i-1][j]==0) {
                    continue;
                }
                int len = Math.min(dp1[i][j-1], dp2[i-1][j]);
                for(int k = len; k >= 1; k--) {
                    if (dp2[i][j-k]>k && dp1[i-k][j]>k) {
                        res = Math.max(res, (k+1)*(k+1));
                        break;
                    }
                }
            }
        }
        return res;
    }
}
~~~


21. 合并两个有序链表
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
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1==null || l2 == null) {
            return l1!=null?l1:l2;
        }
        ListNode newHead = new ListNode(0);
        ListNode temp = newHead;
        while(l1!=null || l2!=null) {
            if (l1 == null) {
                temp.next = l2;
                break;
            }
            if (l2 == null) {
                temp.next = l1;
                break;
            }
            if (l1.val > l2.val) {
                temp.next = l2;
                l2 = l2.next;
            } else {
                temp.next = l1;
                l1 = l1.next;
            }
            temp = temp.next;
        }
        return newHead.next;
    }
}
~~~
