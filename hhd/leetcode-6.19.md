1. 两数之和
~~~java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int i = 0; i < nums.length; i++) {
            Integer index = map.get(target-nums[i]);
            if (index != null) {
                return new int[]{index, i};
            } else {
                map.put(nums[i], i);
            }
        }
        return new int[]{-1, -1};
    }
}
~~~

56. 合并区间
~~~java
class Solution {
    public int[][] merge(int[][] intervals) {
        if (intervals == null || intervals.length == 0) {
            return new int[0][];
        }
        
        Arrays.sort(intervals, (n1, n2) -> {
            if (n1[0] == n2[0]) {
                return n1[1] - n2[1];
            } else {
                return n1[0] - n2[0];
            }
        });
        List<int[]> list = new ArrayList<>();
        list.add(intervals[0]);
        for(int i = 1; i < intervals.length; i++) {
            int[] lastArr = list.get(list.size()-1);
            if (lastArr[1] < intervals[i][0]) {
                list.add(intervals[i]);
            } else {
                if (lastArr[1] < intervals[i][1]) {
                    lastArr[1] = intervals[i][1];
                }
            }
        }
        int[][] res = new int[list.size()][2];
        for(int i = 0; i < list.size(); i++) {
            int[] temp = list.get(i);
            res[i][0] = temp[0];
            res[i][1] = temp[1];
        }
        return res;
    }
}
~~~

4. 寻找两个正序数组的中位数
~~~java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        if (nums1 == null || nums1.length <= 0) {
            if (nums2.length%2==0) {
                return (nums2[nums2.length/2]+nums2[nums2.length/2-1])/2.0;
            } else {
                return nums2[nums2.length/2];
            }
        }
        if (nums2 == null || nums2.length <= 0) {
            if (nums1.length%2==0) {
                return (nums1[nums1.length/2]+nums1[nums1.length/2-1])/2.0;
            } else {
                return nums1[nums1.length/2];
            }
        }
        int m = nums1.length;
        int n = nums2.length;
        if ((m+n)%2 != 0) {
            int k = (m+n)/2+1;
            return getKth(nums1, nums2, k);
        } else {
            int k = (m+n)/2;
            return (getKth(nums1, nums2, k) + getKth(nums1, nums2, k+1))/2.0;
        }
    }

    public double getKth(int[] nums1, int[] nums2, int k) {
        int len1 = nums1.length;
        int len2 = nums2.length;
        int idx1 = 0;
        int idx2 = 0;
        while(true) {
            if (idx1 == len1) {
                return nums2[idx2+k-1];
            }
            if (idx2 == len2) {
                return nums1[idx1+k-1];
            }
            if (k == 1) {
                return Math.min(nums1[idx1], nums2[idx2]);
            }
            int newIdx1 = Math.min(len1, idx1+k/2)-1;
            int newIdx2 = Math.min(len2, idx2+k/2)-1;
            if (nums1[newIdx1] < nums2[newIdx2]) {
                k -= (newIdx1 - idx1 + 1);
                idx1 = newIdx1 + 1;
            } else {
                k -= (newIdx2 - idx2 + 1);
                idx2 = newIdx2+1;
            }
        }
    }
}
~~~

