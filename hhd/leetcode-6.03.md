238. 除自身以外数组的乘积
~~~java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int[] res = new int[n];
        int[] left = new int[n];
        int[] right = new int[n];
        left[0] = nums[0];
        right[n-1] = nums[n-1];
        for(int i = 1; i < n; i++) {
            left[i] = left[i-1]*nums[i];
            right[n-i-1] = right[n-i]*nums[n-i-1];
        }
        for(int i = 0; i < n; i++) {
            res[i] = 1;
            if (i > 0) {
                res[i] *= left[i-1];
            }
            if (i < n - 1) {
                res[i] *= right[i+1];
            }
        }
        return res;
    }
}
~~~



378. 有序矩阵中第K小的元素
~~~java
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        int n = matrix.length;
        int[] arr = new int[k];
        for(int i = 0; i < k; i++) {
            arr[i] = Integer.MAX_VALUE;
        }
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < n; j++) {
                if (matrix[i][j] >= arr[k-1]) {
                    break;
                }
                int index = k-2;
                while(index >= 0 && matrix[i][j] < arr[index]) {
                    arr[index+1] = arr[index];
                    index--;
                }
                arr[index+1] = matrix[i][j];
            }
        }
        return arr[k-1];
    }
}
~~~


352. 将数据流变为多个不相交区间
~~~java
class SummaryRanges {

    List<int[]> list;

    /** Initialize your data structure here. */
    public SummaryRanges() {
        list = new ArrayList<>();
    }
    
    public void addNum(int val) {
        if (list.size() == 0) {
            int[] arr = new int[]{val, val};
            list.add(arr);
        } else {
            Iterator<int[]> iterator =  list.iterator();
            int[] arr = new int[]{val, val};
            boolean flag = true;
            int count = 0;
            while(iterator.hasNext()) {
                int[] inArr = iterator.next();
                if (inArr[0] <= val && inArr[1] >= val) {
                    count++;
                    break;
                }
                if (inArr[0] - val == 1) {
                    count++;
                    if (flag) {
                        flag = false;
                        arr = inArr;
                        arr[0] = val;
                    } else {
                        arr[1] = inArr[1];
                        iterator.remove();
                    }
                    
                }
                if (val - inArr[1] == 1) {
                    count++;
                    if (flag) {
                        flag = false;
                        arr = inArr;
                        arr[1] = val;
                    } else {
                        arr[0] = inArr[0];
                        iterator.remove();
                    }
                    
                }
            }
            if (count == 0) {
                list.add(arr);
            }
        }
    }
    
    public int[][] getIntervals() {
        int[][] res = new int[list.size()][];
        Collections.sort(list, (i1, i2) -> {
            return i1[0] - i2[1];
        });
        
        for(int i = 0; i < list.size(); i++) {
            res[i] = list.get(i);
        }
        return res;
    }
}

/**
 * Your SummaryRanges object will be instantiated and called as such:
 * SummaryRanges obj = new SummaryRanges();
 * obj.addNum(val);
 * int[][] param_2 = obj.getIntervals();
 */
~~~
