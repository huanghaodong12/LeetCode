739. 每日温度
~~~java
class Solution {
    public int[] dailyTemperatures(int[] T) {
        Stack<Integer> stack = new Stack<>();
        int[] res = new int[T.length];
        for(int i = 0; i < T.length; i++) {
            while(!stack.isEmpty() && T[stack.peek()] < T[i]) {
                res[stack.peek()] = i - stack.peek();
                stack.pop();
            }
            stack.push(i);
        }
        return res;
    }
}
~~~

309. 最佳买卖股票时机含冷冻期
~~~java
class Solution {
    public int maxProfit(int[] prices) {
       if (prices.length <= 0) {
           return 0;
       }
       int n = prices.length;
       int[][] dp = new int[n][3];
       dp[0][1] -= prices[0]; 
       for(int i = 1; i < n; i++) {
           dp[i][0] = Math.max(dp[i-1][0], dp[i-1][2]);
           dp[i][1] = Math.max(dp[i-1][1], dp[i-1][0]-prices[i]);
           dp[i][2] = dp[i-1][1] + prices[i];
       }
       return Math.max(dp[n-1][0], dp[n-1][2]);
    }
}
~~~

4. 寻找两个正序数组的中位数
~~~java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int m = nums1.length;
        int n = nums2.length;
        if (n == 0) {
            if (m%2 == 0) {
                return (nums1[m/2]+nums1[m/2-1])/2.0;
            } else {
                return nums1[m/2];
            }
        }
        if (m == 0) {
            if (n%2 == 0) {
                return (nums2[n/2]+nums2[n/2-1])/2.0;
            } else {
                return nums2[n/2];
            }
        }
        int i = 0, j = 0;
        int[] res = new int[(m+n)/2+1];
        int index = 0; 
        while(index < res.length) {
            if (i >= m) {
                res[index++] = nums2[j++];
            } else if(j >= n) {
                res[index++] = nums1[i++];
            } else {
                if (nums1[i] >= nums2[j]) {
                    res[index++] = nums2[j++];
                } else {
                    res[index++] = nums1[i++];
                } 
            }
        }
        if ((m+n)%2==0) {
            return (res[res.length-1] + res[res.length-2])/2.0;
        } else {
            return res[res.length-1];
        }
    }
}
~~~
