面试题11. 旋转数组的最小数字
~~~java
class Solution {
    public int minArray(int[] numbers) {
        if (numbers == null || numbers.length <= 0) {
            return 0;
        }
        int i = 0;
        int j = numbers.length-1;
        while(i < j) {
            int mid = (i+j)/2;
            if (numbers[mid] > numbers[j]) 
                i = mid+1;
            else if (numbers[mid] < numbers[j])
                j = mid;
            else
                j--;
        }
        return numbers[i];
    }
}
~~~

面试题 10.03. 搜索旋转数组
~~~java
class Solution {
    public int search(int[] arr, int target) {
        int i = 0;
        int j = arr.length-1;
        while(i < j) {
            int m = (i+j)/2;
            if (arr[i] < arr[m]) {
                if (arr[i] <= target && arr[m] >= target) {
                    j = m;
                } else {
                    i = m+1;
                }
            } else if (arr[i] > arr[m]) {
                if (arr[m] < target && arr[j] >= target && arr[i] > arr[j]) {
                    i = m+1;
                } else {
                    j = m;
                }
            } else {
                if (arr[i] != target) {
                    i++;
                } else {
                    j = i;
                }
            }
        }
        return arr[i]==target?i:-1;
    }
}
~~~


153. 寻找旋转排序数组中的最小值
~~~java
class Solution {
    public int findMin(int[] nums) {
        if (nums == null || nums.length <= 0) {
            return 0;
        }
        int i = 0;
        int j = nums.length-1;
        while(i < j) {
            int m = (i+j)/2;
            if (nums[m] > nums[j]) {
                i = m+1;
            } else {
                j = m;
            }
        }
        return nums[i];
    }
}
~~~


154. 寻找旋转排序数组中的最小值 II
~~~java
class Solution {
    public int findMin(int[] nums) {
        if (nums == null || nums.length <= 0) {
            return 0;
        }
        int i = 0;
        int j = nums.length-1;
        while(i < j) {
            int m = (i+j)/2;
            if (nums[m] > nums[j]) {
                i = m+1;
            } else if (nums[m] < nums[j]) {
                j = m;
            } else {
                j--;
            }
        }
        return nums[i];
    }
}
~~~
