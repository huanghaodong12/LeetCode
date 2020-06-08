605. 种花问题
~~~java
class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        int count = 0;
        for(int i = 0; i < flowerbed.length; i++) {
            if (flowerbed[i] == 1) {
                count++;
            }
        }
        int[] dp = new int[flowerbed.length+2];
        for(int i = 2; i < dp.length; i++) {
            if (i+1 < dp.length && flowerbed[i-1]==1) {
                dp[i] = Math.max(dp[i-1], dp[i-2]);
            } else {
                dp[i] = Math.max(dp[i-1], dp[i-2]+1);
            }
        }
        return dp[flowerbed.length+1]-count >= n;
    }
}
~~~


23. 合并K个排序链表
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
    public ListNode mergeKLists(ListNode[] lists) {
        ListNode head = new ListNode(0);
        ListNode temp = head;
        while(true) {
            boolean flag = true;
            int keepIndex = 0;            
            for(int i = 0; i < lists.length; i++) {
                if (lists[i] == null) {
                    continue;
                }
                flag = false;
                if (lists[keepIndex]==null || lists[keepIndex].val > lists[i].val) {
                    keepIndex = i;
                }
            }
            if (flag) {
                break;
            }
            temp.next = new ListNode(lists[keepIndex].val);
            temp = temp.next;
            lists[keepIndex] = lists[keepIndex].next;
        }
        
        return head.next;
    }
}
~~~

面试题 17.16. 按摩师
~~~java
class Solution {
    public int massage(int[] nums) {
        if (nums == null || nums.length <= 0) {
            return 0;
        }
        for(int i = 1; i < nums.length; i++) {
            if (i > 1) {
                nums[i] = Math.max(nums[i-1], nums[i-2]+nums[i]);
            } else {
                nums[i] = Math.max(nums[i-1], nums[i]);
            }
        }
        return nums[nums.length-1];
    }
}
~~~

714. 买卖股票的最佳时机含手续费
~~~java
class Solution {
    public int maxProfit(int[] prices, int fee) {
        int keepIdx = 0;
        int n = prices.length;
        int pre = -1;
        int res = 0;
        for(int i = 1; i < n; i++) {
            if (prices[i] < prices[keepIdx]) {
                keepIdx = i;
                continue;
            }
            if (i+1 < n && prices[i] <= prices[i+1]) {
                continue;
            }
            int temp = -1;
            if (pre != -1) {
                temp = Math.max(prices[i]-prices[keepIdx]-fee, prices[i]-prices[pre]);
            } else {
                temp = prices[i]-prices[keepIdx]-fee;
            }
            if (temp >= 0) {
                res += temp;
                pre = i;
                keepIdx = i;
            }
            
        }
        return res;
    }
}
~~~

990. 等式方程的可满足性
~~~java
class Solution {
    public boolean equationsPossible(String[] equations) {
        int[] parent = new int[26];
        for(int i = 0; i < 26; i++) {
            parent[i] = i;
        }
        for(String str : equations) {
            if (str.charAt(1) == '=') {
                int idx1 = str.charAt(0) - 'a';
                int idx2 = str.charAt(3) - 'a';
                union(parent, idx1, idx2);
            }
        }

        for(String str : equations) {
            if (str.charAt(1) == '!') {
                int idx1 = str.charAt(0) - 'a';
                int idx2 = str.charAt(3) - 'a';
                if (finParent(parent, idx1) == finParent(parent, idx2)) {
                    return false;
                }
            }
        }
        return true;
    }

    public void union(int[] parent, int idx1, int idx2) {
        parent[finParent(parent, idx1)] = finParent(parent, idx2);
    }

    public int finParent(int[] parent, int index) {
        while(parent[index] != index) {
            parent[index] = parent[parent[index]];
            index = parent[index];
        }
        return index;
    }
}
~~~


887. 鸡蛋掉落
~~~java
class Solution {
    public int superEggDrop(int K, int N) {
       int[][] memr = new int[K+1][N+1];
       return rec(K, N, memr);
    }


    public int rec(int K, int N, int[][] memr) {
        if (N==0 || N==1 || K==1) {
            return N;
        }
        if (memr[K][N] != 0) {
            return memr[K][N];
        }
        int res = N;
        for(int i = 1; i <= N; i++) {
            memr[K-1][i-1] = rec(K-1, i-1, memr);
            memr[K][N-i] = rec(K, N-i, memr);
            res = Math.min(res, 1 + Math.max(memr[K-1][i-1], memr[K][N-i]));
        }
        return res;
    }
}
~~~

1312. 让字符串成为回文串的最少插入次数
~~~java
class Solution {
    public int minInsertions(String s) {
        int n = s.length();
        int[][] dp = new int[n][n];
        for(int len = 0; len < n; len++) {
            for(int i = 0; i < n-len; i++) {
                int j = i+len;
                if (i == j) {
                    dp[i][j] = 1;
                    continue;
                }
                dp[i][j] = Math.max(dp[i+1][j], dp[i][j-1]);
                if (s.charAt(i) == s.charAt(j)) {
                    dp[i][j] = Math.max(dp[i][j], dp[i+1][j-1]+2);
                }
            }
        }

        return n - dp[0][n-1];
    }
}
~~~
