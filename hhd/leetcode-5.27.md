20. 有效的括号
~~~java
class Solution {
    public boolean isValid(String s) {
        if (s == null || s.length() <= 0) {
            return true;
        }
        char c = s.charAt(0);
        if (s.length()%2==1 || c==')'||c==']'||c=='}') {
            return false;
        }
        Stack<Character> stack =  new Stack<>();
        for(int i = 0; i < s.length(); i++) {
            c = s.charAt(i);
            if (c=='('||c=='['||c=='{') {
                stack.push(c);
                continue;
            }
            if (stack.isEmpty()) {
                return false;
            }
            char pre = stack.pop();
            if ((pre!='('||c!=')')&&(pre!='['||c!=']')&&(pre!='{'||c!='}')) {
                return false;
            }
        }
        return stack.isEmpty();   
    }

}
~~~


22. 括号生成
~~~java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> list = new ArrayList<>();
        Stack<Character> stack = new Stack<>();
        rec(0, 0, list, stack, n*2);
        return list;
    }

    public void rec(int curNum, int lNum, List<String> list, Stack<Character> stack, int n) {
        if (curNum == n) {
            StringBuilder sb = new StringBuilder(n);
            for(Character c : stack) {
                sb.append(c);
            }
            list.add(sb.toString());
            return;
        }
        if (lNum < n/2) {
            stack.push('(');
            rec(curNum+1, lNum+1, list, stack, n);
            stack.pop();
        }
        if (lNum*2 > curNum) {
            stack.push(')');
            rec(curNum+1, lNum, list, stack, n);
            stack.pop();
        }
    }
}
~~~



1096. 花括号展开 II
~~~java
class Solution {
    public List<String> braceExpansionII(String expression) {
        LinkedList<String> queue = new LinkedList<>();
        Set<String> set = new HashSet<>();
        StringBuilder sb = new StringBuilder();
        queue.addLast(expression);

        while(queue.size() > 0) {
            String str = queue.removeFirst();
            if (str.indexOf("{") == -1) {
                set.add(str);
                continue;
            }

            int i = 0;
            int l = 0;
            int r = 0;
            while(i<str.length()) {
                if (str.charAt(i) == '{') {
                    l = i;
                }
                if (str.charAt(i) == '}') {
                    r = i;
                    break;
                }
                i++;
            }

            String pre = str.substring(0, l);
            String next = str.substring(r+1);
            String mid = str.substring(l+1, r);
            String[] arr = mid.split(",");
            for(String s : arr) {
                sb.setLength(0);
                queue.addLast(sb.append(pre).append(s).append(next).toString());
            }
        }
        List<String> list = new ArrayList<>(set);
        Collections.sort(list);
        return list;
    }
}
~~~


