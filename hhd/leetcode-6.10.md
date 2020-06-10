687. 最长同值路径
~~~java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {

    int max = 0;

    public int longestUnivaluePath(TreeNode root) {
        if (root == null) {
            return 0;
        }
        rec(root);
        return max;
    }

    public int rec(TreeNode node) {
        if (node == null) {
            return 0;
        }
        int l = rec(node.left);
        int r = rec(node.right);
        int sum = 0;
        if (node.left != null && node.left.val == node.val) {
            l++;
        } else {
            l = 0;
        }
        if (node.right != null && node.right.val == node.val) {
            r++;
        } else {
            r = 0;
        }
        max = Math.max(max, l+r);
        return Math.max(l, r);
    }
}
~~~

面试题 04.05. 合法二叉搜索树
~~~java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {

    TreeNode pre;
    
    public boolean isValidBST(TreeNode root) {
        return infixOrder(root);
    }

    public boolean infixOrder(TreeNode node) {
        if (node == null) {
            return true;
        }
        boolean result = infixOrder(node.left);
        if (result && (pre==null || pre.val < node.val)) {
            pre = node;
        } else {
            result = false;
        }
        if (result) {
            result = infixOrder(node.right);
        }
        return result;
    }
}
~~~


834. 树中距离之和
~~~java
class Solution {
    int[] count;
    int[] res;
    List<Set<Integer>> list;
    int N;

    public int[] sumOfDistancesInTree(int N, int[][] edges) {
        if (N <= 1) {
            return new int[]{0};
        }
        this.N = N;
        count = new int[N];
        res = new int[N];
        list = new ArrayList<>();
        for(int i = 0; i < N; i++) {
            count[i] = 1;
            list.add(new HashSet<Integer>());
        }
        for(int i = 0; i < N-1; i++) {
            list.get(edges[i][0]).add(edges[i][1]);
            list.get(edges[i][1]).add(edges[i][0]);
        }
        dfs(0, -1);
        dfs2(0, -1);
        return res;
    }


    public void dfs(int node, int par) {
        for(int i : list.get(node)) {
            if (i != par) {
                dfs(i, node);
                count[node] += count[i];
                res[node] +=  (res[i] + count[i]);
            }
        }
    }


    public void dfs2(int node, int par) {
        for(int i : list.get(node)) {
            if (i != par) {
                res[i] =  res[node] + N - 2*count[i];
                dfs2(i, node);
            }
        }
    }
}
~~~
