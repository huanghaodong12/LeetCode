13. 罗马数字转整数
~~~java
class Solution {
    public int romanToInt(String s) {
        int res = 0;
        for(int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (c == 'I') {
                if (i+1<s.length() && s.charAt(i+1)=='V') {
                    res += 4;
                    i++;
                } else if (i+1<s.length() && s.charAt(i+1)=='X') {
                    res += 9;
                    i++;
                } else {
                    res += 1;
                }
            } else if (c == 'V') {
                res += 5;
            } else if (c == 'X') {
                if (i+1<s.length() && s.charAt(i+1)=='L') {
                    res += 40;
                    i++;
                } else if (i+1<s.length() && s.charAt(i+1)=='C') {
                    res += 90;
                    i++;
                } else {
                    res += 10;
                }
            } else if (c == 'L') {
                res += 50;
            } else if (c == 'C') {
                if (i+1<s.length() && s.charAt(i+1)=='D') {
                    res += 400;
                    i++;
                } else if (i+1<s.length() && s.charAt(i+1)=='M') {
                    res += 900;
                    i++;
                } else {
                    res += 100;
                }
            } else if (c == 'D') {
                res += 500;
            } else if (c == 'M') {
                res += 1000;
            }
        } 
        return res;
    }
}
~~~

12. 整数转罗马数字
~~~java
class Solution {
    public String intToRoman(int num) {
        int[] arr = new int[]{1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
        String[] strArr = new String[]{"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"};
        StringBuilder sb = new StringBuilder();
        int index = 0;
        while(num > 0) {
            for(int i = index; i < arr.length; i++) {
                if (num >= arr[i]) {
                    num -= arr[i];
                    index = i;
                    sb.append(strArr[i]);
                    break;
                }
            }
        }
        return sb.toString();
    }
}
~~~



32. 最长有效括号
~~~java
class Solution {
    public int longestValidParentheses(String s) {
        if (s == null || s.length() <= 0) {
            return 0;
        }
        int[] dp = new int[s.length()+1];
        dp[0] = 0;
        dp[1] = 0;
        int res = 0;
        for(int i = 2; i < dp.length; i++) {
            if (s.charAt(i-2)=='(' && s.charAt(i-1)==')') {
                dp[i] = dp[i-2] + 2;
                res = Math.max(res, dp[i]);
            } else if (dp[i-1] > 0 && s.charAt(i-1)==')'&&(i-dp[i-1]-2)>=0 &&s.charAt(i-dp[i-1]-2)=='(') {
                dp[i] = dp[i-1] + 2;
                if (i-dp[i-1]-2 >= 0) {
                    dp[i] += dp[i-dp[i-1]-2];
                }
                res = Math.max(res, dp[i]);
            }
        }
        return res;
    }
}
~~~
