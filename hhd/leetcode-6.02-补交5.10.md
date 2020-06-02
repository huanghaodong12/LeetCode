70. 爬楼梯
~~~java
class Solution {
    public int climbStairs(int n) {
        if (n < 2) {
            return 1;
        }
        int pre1 = 2;
        int pre2 = 1;
        for(int i = 2; i < n; i++) {
            pre1 += pre2;
            pre2 = pre1 - pre2;
        }
        return pre1;
    }
}
~~~

8. 字符串转换整数 (atoi)
~~~java
class Solution {
    public int myAtoi(String str) {
        if (str == null) {
            return 0;
        }
        str = str.trim();
        if (str.length() == 0) {
            return 0;
        }
        char c = str.charAt(0);
        if (c!='-' && c!='+' && !Character.isDigit(c)) {
            return 0;
        }
        boolean flag = true;
        if (c == '-' || c == '+') {
            if (str.length() <= 1 || !Character.isDigit(str.charAt(1))) {
                return 0;
            }
            if (c == '-') {
                flag = false;
            }
            str = str.substring(1);
            str = str.trim();
        }
        int index = 0;
        while(index < str.length()) {
            if (!Character.isDigit(str.charAt(index))) {
                break;
            }
            index++;
        }
        str = str.substring(0, index);
        index = 0;
        while(index < str.length()) {
            if (str.charAt(index) != '0') {
                break;
            }
            index++;
        }
        str = str.substring(index);
        if (!flag && (str.length()>10 || (str.length()==10&&str.compareTo("2147483648")>=0))) {
            return Integer.MIN_VALUE;
        }
        if (flag && (str.length()>10 || (str.length()==10&&str.compareTo("2147483647")>=0))) {
            return Integer.MAX_VALUE;
        }
        int op = 1;
        if (!flag) {
            op = -1;
        }
        if (str.length() == 0) {
            return 0;
        }
        return Integer.parseInt(str) * op;
    }
}
~~~

面试题64. 求1+2+…+n
~~~java
class Solution {
    public int sumNums(int n) {
        boolean flag = n>0 && (n+=sumNums(n-1))>0;
        return n;
    }
}
~~~



37. 解数独
~~~java
class Solution {
    
    char[][] board;
    int n;
    boolean flag = false;

    public void solveSudoku(char[][] board) {
        this.board = board;
        this.n = board.length;
        backtrack(0, 0);
    }


    public void backtrack(int row, int col) {
        int i = row, j = col;
        boolean temp = false;
        for(; i < n; i++) {
            for(; j < n; j++) {
                if (board[i][j] == '.') {
                    temp = true;
                    break;
                }
            }
            if (temp) {
                break;
            }
            j = 0;
        }
        if (i == 9 && j == 0) {
            flag = true;
            return;
        }
        for(int k = 1; k <= 9; k++) {
            if (!check(i, j, k)) {
                continue;
            }
            board[i][j] = (char)(k + '0');
            backtrack(i, j+1);
            if (flag) {
                return;
            }
            board[i][j] = '.';
        }
    }


    public boolean check(int row, int col, int k) {
        char cur = (char)(k + '0');
        for(int i = 0; i < 9; i++) {
            if (board[row][i] == cur) {
                return false;
            }
        }

        for(int i = 0; i < 9; i++) {
            if (board[i][col] == cur) {
                return false;
            }
        }

        row = row/3*3;
        col = col/3*3;
        for(int i = row; i < row+3; i++) {
            for(int j = col; j < col+3; j++) {
                if (board[i][j] == cur) {
                    return false;
                }
            }
        }
        return true;
    }
}
~~~
