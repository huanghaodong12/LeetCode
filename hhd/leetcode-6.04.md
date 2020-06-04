111. 二叉树的最小深度
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
    public int minDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        return getLen(root) + 1;
    }

   
    public int getLen(TreeNode node) {
        if (node.left == null && node.right == null) {
            return 0;
        }
        if (node.left == null) {
            return getLen(node.right) + 1;
        } else if (node.right == null) {
            return getLen(node.left) + 1;
        }
        return Math.min(getLen(node.left), getLen(node.right)) + 1;
    }
}
~~~


1306. 跳跃游戏 III
~~~java
class Solution {
    public boolean canReach(int[] arr, int start) {
        boolean[] isVisited = new boolean[arr.length];
        LinkedList<Integer> list = new LinkedList<>();
        isVisited[start] = true;
        list.addLast(start);
        boolean res = false;
        while(list.size() > 0) {
            int index = list.removeFirst();
            int next = index-arr[index];
            if (next>=0 && arr[next] == 0) {
                res = true;
                break;
            }
            if (next>=0 && !isVisited[next]) {
                isVisited[next] = true;
                list.addLast(next);
            }
            next = index + arr[index];
            if (next<arr.length && arr[next] == 0) {
                res = true;
                break;
            }
            if (next<arr.length && !isVisited[next]) {
                isVisited[next] = true;
                list.addLast(next);
            }
        }
        return res;
    }
}
~~~



847. 访问所有节点的最短路径
~~~java
class Solution {
   
    public int shortestPathLength(int[][] graph) {
        boolean[][] visited = new boolean[graph.length][1<<graph.length];
        int count = 0;
        LinkedList<Node> list = new LinkedList<>();
        for(int i = 0; i < graph.length; i++) {
            list.addLast(new Node(i, 1<<i));
        }
        int state = (1<<graph.length) - 1;
        while(list.size() > 0) {
            int len = list.size();
            while(len-- > 0) {
                Node node = list.removeFirst();
                if (node.state == state) {
                    return count;
                }
                if (visited[node.cur][node.state]) {
                    continue;
                }
                visited[node.cur][node.state] = true;
                for(int next : graph[node.cur]) {
                    list.addLast(new Node(next, (node.state|1<<next)));
                }
            }
            count++;
        }
        return -1;
    }


    class Node {
        int cur;
        int state;

        public Node(int cur, int state) {
            this.cur = cur;
            this.state = state;
        }
    }

    
}
~~~
