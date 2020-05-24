1360. 日期之间隔几天
~~~java
import java.text.SimpleDateFormat;
import java.time.format.DateTimeFormatter;
import java.util.*;


class Solution {
    public int daysBetweenDates(String date1, String date2) {
        long result = 0L;
        try {
            SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
            Date d1 = sdf.parse(date1);
            Date d2 = sdf.parse(date2);
            long t1 = d1.getTime();
            long t2 = d2.getTime();
            if (t1 < t2) {
                result = (t2 - t1) / (1000 * 60 * 60 * 24);
            } else {
                result = (t1 - t2) / (1000 * 60 * 60 * 24);
            }
        } catch (Exception e) {

        }
        return (int) result;
    }
}
~~~




93. 复原IP地址

~~~java
class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<String> list = new ArrayList<>();
        if (s.length() <= 3) {
            return list;
        }

        for(int i = 1; i<=3 && i<s.length()-2; i++) {
            for(int m = i+1; m<=i+3 && m<s.length()-1; m++) {
                for(int n = m+1; n<=m+3 && n<s.length(); n++) {
                    if (s.length() - n > 3) {
                        continue;
                    }
                    String s1 = s.substring(0, i);
                    String s2 = s.substring(i, m);
                    String s3 = s.substring(m, n);
                    String s4 = s.substring(n);
                    if (judge(s1)&&judge(s2)&&judge(s3)&&judge(s4)) {
                        StringBuilder sb = new StringBuilder();
                        sb.append(s1).append(".")
                        .append(s2).append(".")
                        .append(s3).append(".").append(s4);
                        list.add(sb.toString());
                    }
                }
            }
        }
        return list;
    }

    public boolean judge(String s) {
        if (s.length() >= 2 && s.charAt(0) == '0') {
            return false;
        }
        return Integer.parseInt(s)<=255;
    }
}
~~~



1028. 从先序遍历还原二叉树
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
    public TreeNode recoverFromPreorder(String S) {
        if (S == null || S.length() <= 0) {
            return null;
        }
        char[] arr = S.toCharArray();
        int index = 0;
        StringBuilder sb = new StringBuilder();
        while(index < arr.length) {
            if (Character.isDigit(arr[index])) {
                sb.append(arr[index++]);
            } else {
                break;
            }
        }
        TreeNode root = new TreeNode(Integer.parseInt(sb.toString()));
        Map<Integer, TreeNode> map = new HashMap<>();
        map.put(0, root);
        int count = 0;
        for(int i = index; i < arr.length; i++) {
            if (arr[i] == '-') {
                count++;
            } else {
                sb = new StringBuilder();
                while(i<arr.length) {
                    if (Character.isDigit(arr[i])) {
                        sb.append(arr[i++]);
                    } else {
                        break;
                    }
                }
                i--;
                TreeNode node = new TreeNode(Integer.parseInt(sb.toString()));
                TreeNode parent = map.get(count-1);
                if (parent.left == null) {
                    parent.left = node;
                } else {
                    parent.right = node;
                }
                map.put(count, node);
                count=0;
            }
        }
        return root;
    }
}
~~~

