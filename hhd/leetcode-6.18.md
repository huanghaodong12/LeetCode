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

328. 奇偶链表
~~~java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode oddEvenList(ListNode head) {
        ListNode odd = new ListNode(0);
        ListNode even = new ListNode(0);
        ListNode tmpOdd = odd;
        ListNode tmpEven = even;
        boolean flag = true;
        while(head != null) {
            if (flag) {
                tmpOdd.next = head;
                head = head.next;
                tmpOdd = tmpOdd.next;
                tmpOdd.next = null;
            } else {
                tmpEven.next = head;
                head = head.next;
                tmpEven = tmpEven.next;
                tmpEven.next = null;
            }
            flag = !flag;
        }
        tmpOdd.next = even.next;
        return odd.next;
    }
}
~~~

239. 滑动窗口最大值
~~~java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        int n = nums.length;
        int[] res = new int[n-k+1];
        int max = Integer.MIN_VALUE;
        int maxIdx = -1;
        for(int i = 0; i < k-1; i++) {
            if (nums[i] >= max) {
                max = nums[i];
                maxIdx = i;
            }
        }
        for(int i = k-1; i < nums.length; i++) {
            if (nums[i] >= max) {
                res[i-k+1] = nums[i];
                max = nums[i];
                maxIdx = i;
            } else if (i-k<maxIdx) {
                res[i-k+1] = max;
            } else {
                maxIdx = i;
                max = nums[i];
                int temp = i-1;
                while(temp > i-k) {
                    if (nums[temp] > max) {
                        max = nums[temp];
                        maxIdx = temp;
                    }
                    temp--;
                }
                res[i-k+1] = max;
            }
        }
        return res;
    }
}
~~~
