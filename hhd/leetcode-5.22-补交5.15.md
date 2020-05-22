501. 二叉搜索树中的众数
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
    int maxCount = 0;

    public int[] findMode(TreeNode root) {
        Map<Integer, Integer> map = new HashMap<>();
        rec(root, map);
        List<Integer> list = new ArrayList<>();
        for(Map.Entry<Integer, Integer> entry : map.entrySet()) {
            if (entry.getValue() == maxCount) {
                list.add(entry.getKey());
            }
        }
        int[] res = new int[list.size()];
        for(int i = 0; i < list.size(); i++) {
            res[i] = list.get(i);
        }
        return res;
    }

    public void rec(TreeNode node, Map<Integer, Integer> map) {
        if (node == null) {
            return;
        }
        int value = node.val;
        if (map.get(value) == null) {
            map.put(value, 1);
            maxCount = Math.max(maxCount, 1);
        } else {
            map.put(value, map.get(value)+1);
            maxCount = Math.max(maxCount, map.get(value));
        }
        rec(node.left, map);
        rec(node.right, map);
    }
}
~~~


94. 二叉树的中序遍历
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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        infixOrder(root, list);
        return list;
    }

    public void infixOrder(TreeNode node, List<Integer> list) {
        if (node == null) {
            return;
        }
        infixOrder(node.left, list);
        list.add(node.val);
        infixOrder(node.right, list);
    }
}
~~~


65. 有效数字
~~~java
class Solution {
    public boolean isNumber(String s) {
        if (s==null || s.length()==0 || (s.length()==1&&!Character.isDigit(s.charAt(0)))) {
            return false;
        }
        s = s.trim();
        if (s.charAt(0)=='+' || s.charAt(0)=='-') {
            s = s.substring(1);
        }
        boolean result = false;
        int index = s.indexOf("e");
        if (index == -1) {
            
            result = s.matches("\\d+[.]{0,1}") || s.matches("\\d*\\.\\d+");
        } else {
            result = s.matches("\\d+[.]{0,1}[e][-+]{0,1}\\d+") || s.matches("\\d*\\.\\d+[e][-+]{0,1}\\d+");
        }
        return result;
    }
}
~~~
