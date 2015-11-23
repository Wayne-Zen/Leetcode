[Link](https://leetcode.com/problems/n-queens/)

* 注意对角线

```java
public class Solution {
    public List<List<String>> solveNQueens(int n) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        List<Integer> now = new ArrayList<Integer>();
        boolean[] visited = new boolean[n];
        help(res, now, n, visited);
        List<List<String>> strRes = parse(res, n);
        return strRes;
    }
    
    private List<List<String>> parse(List<List<Integer>> res, int n) {
        List<List<String>> strRes = new ArrayList<List<String>>();
        for (int i = 0; i < res.size(); i++) {
            List<String> sub = new ArrayList<String>();
            char[] arr = new char[n];
            Arrays.fill(arr, '.');
            for (int j = 0; j < res.get(0).size(); j++) {
                int loc = res.get(i).get(j);
                arr[loc] = 'Q';
                String s = String.valueOf(arr);
                arr[loc] = '.';
                sub.add(s);
            }
            strRes.add(sub);
        }
        return strRes;
    }
    
    private void help(List<List<Integer>> res,
                      List<Integer> now, int n,
                      boolean[] visited) {
        if (now.size() == n) {
            res.add(new ArrayList<Integer>(now));
            return;
        }   
        for (int i = 0; i < n; i++) {
            if (visited[i] || !diagCheck(now, i, n)) {
                continue;
            }
            now.add(i);
            visited[i] = true;
            help(res, now, n, visited);
            now.remove(now.size() - 1);
            visited[i] = false;
        }
    }
    
    private boolean diagCheck(List<Integer> now, int index, int n) {
        for (int i = 0; i < now.size(); i++) {
            int row1 = i;
            int col1 = now.get(i);
            int row2 = now.size();
            int col2 = index;
            if (row2 - row1 == col2 - col1 || row2 - row1 == col1 - col2) {
                return false;
            }
        }
        return true;
    }
}
```
