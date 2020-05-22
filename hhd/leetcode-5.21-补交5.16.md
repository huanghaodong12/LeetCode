39. 组合总和
~~~java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> list = new ArrayList<>();
        if (candidates == null || candidates.length <= 0) {
            return list;
        }
        Arrays.sort(candidates);
        LinkedList<Integer> link = new LinkedList<>();
        rec(candidates, 0, target, 0, link, list);
        return list;
    }


    public void rec (int[] candidates, int startIdx, int target, int sum, LinkedList<Integer> link, List<List<Integer>> list) {
        if (startIdx>=candidates.length || sum > target) {
            return;
        }
        if (sum == target) {
            List<Integer> temp = new ArrayList<>(link.size());
            for(Integer i: link) {
                temp.add(i);
            }
            list.add(temp);
            return;
        }
        for(int i = startIdx; i < candidates.length; i++) {
            if (candidates[i] > target) {
                break;
            }
            link.addLast(candidates[i]);
            rec(candidates, i, target, sum+candidates[i], link, list);
            link.removeLast();
        }
    }
}
~~~


面试题63. 股票的最大利润
~~~java
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length <= 0) {
            return 0;
        }
        int max = 0;
        int keepMin = prices[0];
        for (int i = 1; i < prices.length; i++) {
            max = Math.max(max, prices[i]-keepMin);
            keepMin = Math.min(keepMin, prices[i]);
        }
        return max;
    }
}
~~~


233. 数字 1 的个数
~~~java
class Solution {
    public int countDigitOne(int n) {
        int sum = 0;
        if (n <= 0) {
            return sum;
        }
        if (n < 10) {
            return 1;
        }
        int pow = 1;
        while(n/pow >= 10) {
            pow *= 10;
        }
        return (n/pow>1?pow:(n%pow+1)) 
        + countDigitOne(n%pow) 
        + (n/pow)*countDigitOne(pow-1);
    }
}
~~~
