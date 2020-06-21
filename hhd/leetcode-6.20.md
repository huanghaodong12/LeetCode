234. 回文链表
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
    public boolean isPalindrome(ListNode head) {
        ListNode temp = head;
        int count = 0;
        while(temp != null) {
            count++;
            temp = temp.next;
        }
        ListNode re = new ListNode(0);
        int div = count/2;
        while(div > 0) {
            temp = head;
            head = head.next;
            temp.next = re.next;
            re.next = temp;
            div--;
        }
        if (count%2 != 0) {
            head = head.next;
        }
        temp = re.next;
        while(temp != null) {
            if (temp.val != head.val) {
                return false;
            }
            temp = temp.next;
            head = head.next;
        }
        return true;
    }
}
~~~


162. 寻找峰值
~~~java
class Solution {
    public int findPeakElement(int[] nums) {
        int l = 0;
        int r = nums.length - 1;
        while(l < r) {
            int mid = (l+r)/2;
            if (nums[mid] > nums[mid+1]) {
                r = mid;
            } else {
                l = mid+1;
            }
        }
        return r;
    }
}
~~~

329. 矩阵中的最长递增路径
~~~java
class Solution {

    boolean[][] memory;
    int[][] keep;
    int row;
    int col;

    public int longestIncreasingPath(int[][] matrix) {
        if (matrix == null || matrix.length <= 0) {
            return 0;
        }
        row = matrix.length;
        col = matrix[0].length;
        memory = new boolean[row][col];
        keep = new int[row][col];
        int max = 0;
        for(int i = 0; i < row; i++) {
            for(int j = 0; j < col; j++) {
                max = Math.max(max, dfs(matrix, i, j));
            }
        }
        // for(int i = 0; i < row; i++) {
        //     System.out.println(Arrays.toString(keep[i]));
        // }
        return max;
    }


    public int dfs(int[][] matrix, int i, int j) {
        if (memory[i][j]) {
            return keep[i][j];
        }
        memory[i][j] = true;
        int res = 1;
        if (i-1>=0 && matrix[i-1][j] > matrix[i][j]) {
            res = Math.max(res, dfs(matrix, i-1, j) + 1);
        }
        if (i+1<row && matrix[i+1][j] > matrix[i][j]) {
            res = Math.max(res, dfs(matrix, i+1, j) + 1);
        }
        if (j-1>=0 && matrix[i][j-1] > matrix[i][j]) {
            res = Math.max(res, dfs(matrix, i, j-1) + 1);
        }
        if (j+1<col && matrix[i][j+1] > matrix[i][j]) {
            res = Math.max(res, dfs(matrix, i, j+1) + 1);
        }
        keep[i][j] = res;
        return res;
    }
}
~~~
