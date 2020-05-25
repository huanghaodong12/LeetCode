146. LRU缓存机制
~~~java
class LRUCache {

    class DoubleLink {
        DoubleLink pre;
        DoubleLink next;
        Integer key;
        Integer value;

        public DoubleLink() {
        }

        public DoubleLink(Integer key, Integer value) {
            this.key = key;
            this.value = value;
        }
        
    }
    
    private Map<Integer, DoubleLink> map;
    private Integer capacity;
    private DoubleLink head;
    private DoubleLink tail;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.map = new HashMap<>(capacity*2);
        head = new DoubleLink();
        tail = new DoubleLink();
        head.next = tail;
        tail.pre = head;
    }
    
    public int get(int key) {
        DoubleLink node = map.get(key);
        if (node == null) {
            return -1;
        }
        removeAndAddToHead(node);
        return node.value;
    }
    
    public void put(int key, int value) {
        DoubleLink node = map.get(key);
        if (node != null) {
            removeAndAddToHead(node);
            node.value = value;
            return;
        }
        if (capacity == map.size()) {
            node = tail.pre;
            remove(node);
            map.remove(node.key);
        }
        node = new DoubleLink(key, value);
        map.put(key, node);
        addToHead(node);
    }

    public void removeAndAddToHead(DoubleLink node) {
        remove(node);
        addToHead(node);
    }

    public void addToHead(DoubleLink node) {
        node.next = head.next;
        head.next.pre = node;
        head.next = node;
        node.pre = head;
    }

    public void remove(DoubleLink node) {
        node.pre.next = node.next;
        node.next.pre = node.pre;
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
~~~


11. 盛最多水的容器
~~~java
class Solution {
    public int maxArea(int[] height) {
        int res = 0;
        int l = 0;
        int r = height.length-1;
        while(l < r) {
            if (height[l] < height[r]) {
                res = Math.max(res, (r-l)*height[l]);
                l++;
            } else {
                res = Math.max(res, (r-l)*height[r]);
                r--;
            }
        }
        return res;
    }
}
~~~


72. 编辑距离
~~~java
class Solution {
    public int minDistance(String word1, String word2) {
        int[][] dp = new int[word1.length()+1][word2.length()+1];
        for(int j=1; j<dp[0].length; j++) {
            dp[0][j] = dp[0][j-1]+1;
        }
        for(int i=1; i<dp.length; i++) {
            dp[i][0] = dp[i-1][0]+1;
        }
        for(int i=1; i<=word1.length(); i++) {
            for(int j=1; j<=word2.length(); j++) {
                if (word1.charAt(i-1) == word2.charAt(j-1)) {
                    dp[i][j] = dp[i-1][j-1];
                } else {
                    dp[i][j] = Math.min(dp[i-1][j-1], 
                            Math.min(dp[i-1][j], dp[i][j-1])) + 1;
                }
            }
        }
        return dp[word1.length()][word2.length()];
    }
}
~~~
