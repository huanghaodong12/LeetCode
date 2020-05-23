617. 合并二叉树
~~~java
class Solution {
    public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
        if (t1 == null && t2 == null) {
            return null;
        }
        if (t1 == null || t2 == null) {
            return t1!=null?t1:t2;
        }
        int val = t1.val + t2.val;
        TreeNode root = new TreeNode(val);
        root.left = mergeTrees(t1.left, t2.left);
        root.right = mergeTrees(t1.right, t2.right);
        return root;
    }
}
~~~



102. 二叉树的层序遍历
~~~java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> list = new ArrayList<>();
        if (root == null) {
            return list;
        }
        LinkedList<TreeNode> treeNodeList = new LinkedList<>();
        treeNodeList.add(root);
        while(treeNodeList.size() > 0) {
            int length = treeNodeList.size();
            List<Integer> temp = new ArrayList<>();
            for(int i = 0; i < length; i++) {
                TreeNode node = treeNodeList.removeFirst();
                temp.add(node.val);
                if (node.left != null) {
                    treeNodeList.add(node.left);
                }
                if (node.right != null) {
                    treeNodeList.add(node.right);
                }
            }
            list.add(temp);
        }
        return list;
    }
}
~~~



145. 二叉树的后序遍历

递归方案：
~~~java
class Solution {

    

    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        suffixOrder(root, list);
        return list;
    }

    public void suffixOrder(TreeNode node, List<Integer> list) {
        if (node == null) {
            return;
        }
        suffixOrder(node.left, list);
        suffixOrder(node.right, list);
        list.add(node.val);
    }
}
~~~

迭代方案：
~~~java
class Solution {

    

    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> list = new ArrayList<>();
        if (root == null) {
            return list;
        }
        LinkedList<TreeNode> link = new LinkedList<>();
        link.add(root);
        while(link.size() > 0) {
            TreeNode node =  link.removeLast();
            list.add(node.val);
            if (node.left != null) {
                link.add(node.left);
            }
            if (node.right != null) {
                link.add(node.right);
            }
        }
        Collections.reverse(list);
        return list;
    }

}
~~~
