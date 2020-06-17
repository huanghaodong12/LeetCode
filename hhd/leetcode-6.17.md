997. 找到小镇的法官
~~~java
class Solution {
    public int findJudge(int N, int[][] trust) {
        if (N == 1 && trust.length <= 0) {
            return 1;
        } else if (N > 1 && trust.length <= 0) {
            return -1;
        }
        int[][] keep = new int[N][2];
        for(int i = 0; i < trust.length; i++) {
            int start = trust[i][0];
            int end = trust[i][1];
            keep[start-1][1]++;
            keep[end-1][0]++;
        }
        int res = -1;
        for(int i = 0; i < N; i++) {
            if (keep[i][0] == N-1 && keep[i][1] == 0) {
                if (res == -1) {
                    res = i+1;
                } else {
                    res = -1;
                    break;
                }
            }
        }
        return res;
    }
}
~~~

207. 课程表
~~~java
class Solution {
    int[][] memry;

    public boolean canFinish(int numCourses, int[][] prerequisites) {
        List<Set<Integer>> list = new ArrayList<>();
        memry = new int[numCourses][numCourses];
        for(int i = 0; i < numCourses; i++) {
            list.add(new HashSet<Integer>());
        }
        for(int i = 0; i < prerequisites.length; i++) {
            int row = prerequisites[i][0];
            int col = prerequisites[i][1];
            list.get(row).add(col);
        }
        for(int i = 0; i < numCourses-1; i++) {
            if (!dfs(i, list, i)) {
                return false;
            }
        }
        return true;     
    } 

    public boolean dfs(int cur, List<Set<Integer>> list, int start) {
        if (memry[cur][start] == 2) {
            return true;
        } else if (memry[cur][start] == 1) {
            return false;
        } 
        memry[cur][start] = 1;
        Set<Integer> set = list.get(cur);
        if (set.size() == 0) {
            return true;
        }
        boolean res = true;
        for(Integer i : set) {
            if (list.get(i).contains(start)) {
                res = false;
                break;
            }
            // memry[i][start] = 1;
            res = dfs(i, list, start);
            memry[i][start] = res?2:1;
            if (!res) {
                break;
            }
        }
        memry[cur][start] = res?2:1;
        return res;
    }
}
~~~

46. 全排列
~~~java
class Solution {
    
    List<List<Integer>> list;
    boolean[] visited;

    public List<List<Integer>> permute(int[] nums) {
        list = new ArrayList<>();
        visited = new boolean[nums.length];
        LinkedList<Integer> keep = new LinkedList<>();
        fullSort(nums, keep);
        return list;
    }

    public void fullSort(int[] nums,  LinkedList<Integer> keep) {
        if (keep.size() == nums.length) {
            List<Integer> temp = new ArrayList<>();
            for(Integer i : keep) {
                temp.add(i);
            }
            list.add(temp);
            return;
        }
        for(int i = 0; i < nums.length; i++) {
            if (!visited[i]) {
                keep.addLast(nums[i]);
                visited[i] = true;
                fullSort(nums, keep);
                keep.removeLast();
                visited[i] = false;
            }
        }
    }
}
~~~

47. 全排列 II
~~~java
class Solution {

    List<List<Integer>> list;
    boolean[] visited;

    public List<List<Integer>> permuteUnique(int[] nums) {
        list = new ArrayList<>();
        visited = new boolean[nums.length];
        LinkedList<Integer> keep = new LinkedList<>();
        Arrays.sort(nums);
        fullSort(nums, keep);
        return list;
    }


    public void fullSort(int[] nums, LinkedList<Integer> keep) {
        if (nums.length == keep.size()) {
            list.add(new ArrayList<Integer>(keep));
            return;
        }
        for(int i = 0; i < nums.length; i++) {
            if (!visited[i]) {
                if (i>0 && nums[i]==nums[i-1] && !visited[i-1]) {
                    continue;
                }
                visited[i] = true;
                keep.addLast(nums[i]);
                fullSort(nums, keep);
                visited[i] = false;
                keep.removeLast();
            }
        }
    }
}
~~~


996. 正方形数组的数目
~~~java
class Solution {
    int count = 0;
    public int numSquarefulPerms(int[] A) {
        Arrays.sort(A);
        boolean[] visited = new boolean[A.length];
        dfs(A, visited, 0, 0);
        return count;
    }

    public void dfs(int[] A, boolean[] visited, int len, int pre) {
        if (A.length == len) {
            count++;
            return;
        }
        for(int i = 0; i < A.length; i++) {
            if (!visited[i]) {
                if (len > 0) {
                    if ((long)Math.sqrt(pre+A[i])!=Math.sqrt(pre+A[i]) 
                            || ( i>0 && A[i]==A[i-1] && visited[i-1])) {
                        continue;
                    }
                }
                visited[i] = true;
                dfs(A, visited, len+1, A[i]);
                visited[i] = false;
            }
        }
    }
}
~~~
