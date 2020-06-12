628. 三个数的最大乘积
~~~java
class Solution {
    public int maximumProduct(int[] nums) {
        int min1 = Integer.MAX_VALUE;
        int min2 = Integer.MAX_VALUE;
        int max1 = Integer.MIN_VALUE;
        int max2 = Integer.MIN_VALUE;
        int max3 = Integer.MIN_VALUE;
        for(int i = 0; i < nums.length; i++) {
            if (nums[i] < min1) {
                min2 = min1;
                min1 = nums[i];
            } else if (nums[i] < min2) {
                min2 = nums[i];
            }

            if (nums[i] > max1) {
                max3 = max2;
                max2 = max1;
                max1 = nums[i];
            } else if (nums[i] > max2) {
                max3 = max2;
                max2 = nums[i];
            } else if (nums[i] > max3) {
                max3 = nums[i];
            }
        }
        return Math.max(min1*min2*max1, max1*max2*max3);
    }
}
~~~


1333. 餐厅过滤器
~~~java
class Solution {
    public List<Integer> filterRestaurants(int[][] restaurants, int veganFriendly, int maxPrice, int maxDistance) {
        return Arrays.stream(restaurants)
        .filter(item -> {
            if (veganFriendly == 1)
                return item[2]==veganFriendly;
            return true;
        })
        .filter(item -> item[3] <= maxPrice)
        .filter(item -> item[4] <= maxDistance)
        .sorted((item1, item2) -> {
            if (item1[1] == item2[1]) {
                return item2[0] - item1[0];
            } else {
                return item2[1] - item1[1];
            }
        })
        .map(item -> item[0])
        .collect(Collectors.toList());
    }
}
~~~


1. 两数之和
~~~java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int n = nums.length;
        Map<Integer, Integer> map = new HashMap<>();
        for(int i = 0; i < n; i++) {
            Integer j = map.get(target-nums[i]);
            if (j != null) {
                return new int[]{j, i}; 
            } else {
                map.put(nums[i], i);
            }
        }
        return new int[]{0, 0};
    }
}
~~~


15. 三数之和
~~~java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        int n = nums.length;
        List<List<Integer>> list = new ArrayList<>();
        if (n < 3) {
            return list;
        }
        Arrays.sort(nums);
        for(int i = 0; i < n; i++) {
            if (nums[i] > 0) {
                break;
            }
            if (i > 0 && nums[i]==nums[i-1]){
                continue;
            }
            int l = i+1;
            int r = n-1;
            while(l < r) {
                if (nums[i]+nums[l]+nums[r]==0) {
                    List<Integer> temp = new ArrayList<>();
                    
                    while(l+1 < r && nums[l]==nums[l+1]){
                        l++;
                    }
                    while(l < r-1 && nums[r]==nums[r-1]){
                        r--;
                    }
                    temp.add(nums[i]);
                    temp.add(nums[l]);
                    temp.add(nums[r]);
                    list.add(temp);
                    l++;
                    r--;
                } else if (nums[i]+nums[l]+nums[r] > 0) {
                    r--;
                } else {
                    l++;
                }
            }
        }
        return list;
    }
}


class Node {
    Integer l1;
    Integer l2;
    Integer l3;

    public Node (Integer l1, Integer l2, Integer l3) {
        if (l1 < l2) {
            int temp = l1;
            l1 = l2;
            l2 = temp;
        } 
        if (l1 < l3) {
            int temp = l1;
            l1 = l3;
            l3 = temp;
        }
        if (l2 < l3) {
            int temp = l2;
            l2 = l3;
            l3 = temp;
        }
        this.l1 = l1;
        this.l2 = l2;
        this.l3 = l3;
    } 

    @Override
    public int hashCode() {
        int result = l1 != null ? l1.hashCode() : 0;
        result = 31 * result + (l2 != null ? l2.hashCode() : 0);
        result = 31 * result + (l3 != null ? l3.hashCode() : 0);
        return result;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Node node = (Node) o;
        if (this.l1==node.l1 && this.l2==node.l2 && this.l3==node.l3) {
            return true;
        }
        return false;
    }
}
~~~

面试题 17.19. 消失的两个数字
~~~java
class Solution {
    public int[] missingTwo(int[] nums) {
        if (nums == null) {
            return new int[2];
        }
        long n = nums.length+2;
        long sum = 0;
        for(int i = 0; i < nums.length; i++) {
            sum += nums[i];
        }
        long div = n*(n+1)/2 - sum;
        long limit = div/2;
        sum = 0;
        for(int i = 0; i < nums.length; i++) {
            if (nums[i] <= limit) {
                sum += nums[i];
            } 
        }
        limit = limit*(limit+1)/2 - sum;
        return new int[]{(int)limit, (int)(div-limit)};
    }
}
~~~
