[Link](https://leetcode.com/problems/maximal-rectangle/)

```java
public class Solution {
    public int maximalRectangle(char[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return 0;
        }
        int m = matrix.length;
        int n = matrix[0].length;
        int[] h = new int[n];
        int max = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (matrix[i][j] == '0') {
                    h[j] = 0;
                } else {
                    h[j]++;
                }
            }
            max = Math.max(max, hist(h));
        }
        return max;
    }
    
    private int hist(int[] h) {
        int max = 0;
        int[][] bound = new int[h.length][2];
        Stack<Integer> stack = new Stack<Integer>();
        for (int in = 0; in < h.length; in++) {
            while (!stack.isEmpty() && h[stack.peek()] >= h[in]) {
                int out = stack.pop();
                bound[out][1] = in;
                int area = h[out] * (bound[out][1] - bound[out][0] - 1);
                max = Math.max(max, area);
            } 
            if (stack.isEmpty()) {
                bound[in][0] = -1;
            } else {
                bound[in][0] = stack.peek();
            }
            stack.push(in);
        }
        while (!stack.isEmpty()) {
            int out = stack.pop();
            bound[out][1] = h.length;
            int area = h[out] * (bound[out][1] - bound[out][0] - 1);
            max = Math.max(max, area);
        }
        return max;
    }
}
```
