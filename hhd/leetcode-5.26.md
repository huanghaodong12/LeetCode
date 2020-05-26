287. 寻找重复数
~~~java
class Solution {
    public int findDuplicate(int[] nums) {
        int slow = 0;
        int fast = 0;
        while(true) {
            slow = nums[slow];
            fast = nums[nums[fast]];
            if (slow == fast) {
                break;
            }
        }
        slow = 0;
        while(slow != fast) {
            slow = nums[slow];
            fast = nums[fast];
        }
        return fast;
    }
}
~~~


面试题13. 机器人的运动范围
~~~java
class Solution {
    public int movingCount(int m, int n, int k) {
        boolean[][] flag = new boolean[m][n];
        return dfs(0, 0, k, flag);
    }

    public int dfs(int i, int j, int k, boolean[][] flag) {
        int m = flag.length;
        int n = flag[0].length;
        if (i<0||i>=m||j<0||j>=n||flag[i][j]||(i/10+i%10+j/10+j%10)>k) {
            return 0;
        }
        flag[i][j] = true;
        return dfs(i+1,j,k,flag)+dfs(i-1,j,k,flag)
            +dfs(i,j-1,k,flag)+dfs(i,j+1,k,flag)+1;
    }
}
~~~

142. 环形链表 II
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
    public ListNode detectCycle(ListNode head) {
        if (head==null) {
            return null;
        }
        ListNode slow = head;
        ListNode fast = head;
        while(true) {
            if (fast.next == null || fast.next.next == null) {
                return null;
            }
            fast = fast.next.next;
            slow = slow.next;
            if (fast == slow) {
                break;
            }
        }
        fast = head;
        while(fast != slow) {
            fast = fast.next;
            slow = slow.next;
        }
        return fast;
    }
}
~~~
