507. 完美数
~~~java
class Solution {
    public boolean checkPerfectNumber(int num) {
        int count = 1;
        int i = 2;
        int len = num/2;
        while(i < len) {
            if (num % i == 0) {
                count += (num/i + i);
                len = num/i;
            }
            i++;
        }
        if (count != num || num == 1) {
            return false;
        } else {
            return true;
        }
    }
}
~~~

869. 重新排序得到 2 的幂
~~~java
class Solution {
    public boolean reorderedPowerOf2(int N) {
        int pow = 1;
        int len = 0;
        while(N >= pow) {
            pow *= 10;
            len++;
        }
        pow /= 10;
        int[] arr = new int[len];
        int index = 0;
        int keep = N;
        while(N > 0) {
            arr[index++] = N%10;
            N /= 10;
        }
        Set<Integer> set = new HashSet<>();
        int temp = 1;
        while(temp <= pow*10) {
            if (temp >= pow) {
                set.add(temp);
            }
            temp *= 2;
        }
        Stack<Integer> stack = new Stack<>();
        if (set.contains(keep)) {
            return true;
        }
        return rec(arr, stack, set, len);
    }

    public boolean rec(int[] arr, Stack<Integer> stack, Set<Integer> set, int len) {
        if (arr.length == 0) {
            int num = 0;
            for(int i = 0; i < stack.size(); i++) {
                num *= 10;
                num += stack.get(i);
            }
            if (set.contains(num)) {
                return true;
            }
            return false;
        }

        for(int i = 0; i < arr.length; i++) {
            if (arr[i] == 0 && arr.length == len) {
                continue;
            }
            stack.push(arr[i]);
            int[] subArr = new int[arr.length-1];
            for(int m = 0, n = 0; m < subArr.length; m++, n++) {
                if (i == n) {
                    n++;
                }
                subArr[m] = arr[n];
            }
            if(rec(subArr, stack, set, len)) {
                return true;
            }
            stack.pop();
        }
        return false;
    }
}
~~~


458. 可怜的小猪
~~~java
class Solution {
    public int poorPigs(int buckets, int minutesToDie, int minutesToTest) {
        int num = minutesToTest/minutesToDie + 1;
        return (int)Math.ceil(Math.log(buckets)/Math.log(num));
    }
}
~~~
