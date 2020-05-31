148. 排序链表
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
    public ListNode sortList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode res = new ListNode(0);
        res.next = head;
        ListNode temp = head;
        int length = 0;
        while(temp != null) {
            length++;
            temp = temp.next;
        }
        
        for(int i = 1; i < length; i*=2) {
            ListNode tail = res;
            ListNode cur = res.next;
            while(cur != null) {
                ListNode l = cur;
                ListNode r = getCutNode(cur, i);
                cur = getCutNode(r, i);
                tail.next = merge(l, r);
                while(tail.next != null) {
                    tail = tail.next;
                }
            }
        }
        return res.next;
    }

    public ListNode getCutNode(ListNode node, int len) {
        for(int i = 1; i < len; i++) {
            if (node == null) {
                return null;
            }
            node = node.next;
        }
        if (node == null) {
            return null;
        }
        ListNode next = node.next;
        node.next = null;
        return next;
    }


    public ListNode merge(ListNode l, ListNode r) {
        if (r == null) {
            return l;
        }
        ListNode head = new ListNode(0);
        ListNode temp = head;
        while(l != null || r != null) {
            if (l == null) {
                temp.next = r;
                break;
            }
            if (r == null) {
                temp.next = l;
                break;
            }
            if (l.val > r.val) {
                temp.next = r;
                r = r.next;
                temp = temp.next;
            } else {
                temp.next = l;
                l = l.next;
                temp = temp.next;
            }
        }
        return head.next;
    }
}
~~~



25. K 个一组翻转链表
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
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode res = new ListNode(0);
        ListNode slow = head;
        ListNode fast = head;
        ListNode tail = res;
        while(true) {
            int i = 1;
            while(i < k && fast != null) {
                fast = fast.next;
                i++;
            }
            if (fast == null) {
                tail.next = slow;
                break;
            }
            fast = fast.next;
            i = 1;
            while(i <= k) {
                ListNode temp = slow;
                slow = slow.next;
                temp.next = tail.next;
                tail.next = temp;
                i++;
            }
            while(tail.next != null) {
                tail = tail.next;
            }
        }
        return res.next;
    }
}
~~~


546. 移除盒子
~~~java
class Solution {
    public int removeBoxes(int[] boxes) {
        return calculatePoints(boxes, 0, boxes.length-1, 0, new int[100][100][100]);
    }

    public int calculatePoints(int[] boxes, int l, int r, int k, int[][][] dp) {
        if (l > r) {
            return 0;
        }
        if (dp[l][r][k] > 0) {
            return dp[l][r][k];
        }
        while(r > l && boxes[r] == boxes[r-1]) {
            r--;
            k++;
        }
        dp[l][r][k] = calculatePoints(boxes, l, r-1, 0, dp) + (k+1)*(k+1);
        
        for(int i = l; i < r; i++) {
            if (boxes[i] == boxes[r]) {
                dp[l][r][k] = Math.max(dp[l][r][k], 
                    calculatePoints(boxes, l, i, k+1, dp) 
                    + calculatePoints(boxes, i+1, r-1, 0, dp));
            }
        }

        return dp[l][r][k];
    }
}
~~~
