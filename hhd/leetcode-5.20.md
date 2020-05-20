463. 岛屿的周长
~~~java
class Solution {
    public int islandPerimeter(int[][] grid) {
        int count = 0;
        for(int i = 0; i < grid.length; i++) {
            for(int j = 0; j < grid[i].length; j++) {
                if (grid[i][j] == 0) {
                    continue;
                }
                if (i-1<0 || grid[i-1][j]==0) {
                    count++;
                }
                if (i+1>=grid.length || grid[i+1][j]==0) {
                    count++;
                }
                if (j-1<0 || grid[i][j-1]==0) {
                    count++;
                }
                if (j+1>=grid[i].length || grid[i][j+1] == 0) {
                    count++;
                }
            }
        }
        return count;
    }
}
~~~

701. 二叉搜索树中的插入操作
~~~java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) {
            return new TreeNode(val);
        }
        TreeNode newRoot = new TreeNode(root.val);
        generator(root, newRoot);
        add(newRoot, val);
        return newRoot;
    }

    public void add(TreeNode node, int val) {
        
        if (node.val > val) {
            if (node.left == null) {
                node.left = new TreeNode(val);
            } else {
                add(node.left, val);
            }
        } else {
            if (node.right == null) {
                node.right = new TreeNode(val);
            } else {
                add(node.right, val);
            }
        }
    }

    public void generator(TreeNode oldNode, TreeNode newNode) {
        if (oldNode.left==null && oldNode.right==null) {
            return;
        }
        if (oldNode.left != null) {
            newNode.left = new TreeNode(oldNode.left.val);
            generator(oldNode.left, newNode.left);
        }
        if (oldNode.right != null) {
            newNode.right = new TreeNode(oldNode.right.val);
            generator(oldNode.right, newNode.right);
        }
    }
}
~~~


1335. 工作计划的最低难度
~~~java
class Solution {
    public int minDifficulty(int[] jobDifficulty, int d) {
        if (jobDifficulty.length < d) {
            return -1;
        }
        int[][] map = new int[jobDifficulty.length+1][jobDifficulty.length+1];
        for(int i = 1; i <= jobDifficulty.length; i++) {
            map[i][i] = jobDifficulty[i-1];
            for(int j = i+1; j <= jobDifficulty.length; j++) {
                map[i][j] = Math.max(map[i][j-1], jobDifficulty[j-1]);
            }
        }
        int[][] dp = new int[d+1][jobDifficulty.length+1];
        dp[1][1] = jobDifficulty[0];
        for(int i = 2; i < dp[1].length; i++) {
            dp[1][i] = Math.max(dp[1][i-1], jobDifficulty[i-1]);
        }
        for(int i = 2; i <= d; i++) {
            for(int j = i; j <= jobDifficulty.length; j++) {
                dp[i][j] = Integer.MAX_VALUE;
                for(int k=i-1; k<j; k++) {
                    dp[i][j]=Math.min(dp[i][j], dp[i-1][k]+map[k+1][j]);
                }
            }
        }
        return dp[d][jobDifficulty.length];
    }
}
~~~
