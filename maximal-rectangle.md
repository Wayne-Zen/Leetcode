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

    public int hist(int[] height) {
        if (height == null || height.length == 0) {
            return 0;
        }
        // store index
        Stack<Integer> stack = new Stack<Integer>();
        int[][] bound = new int[height.length][2];
        int max = 0;
        for (int in = 0; in < height.length; in++) {
            while (!stack.isEmpty() && height[stack.peek()] >= height[in]) {
                int out = stack.pop();
                bound[out][1] = in;
                max = Math.max(max, (bound[out][1] - bound[out][0] - 1) * height[out]);
            }
            bound[in][0] = stack.isEmpty() ? -1 : stack.peek();
            stack.push(in);
        }
        while (!stack.isEmpty()) {
            int out = stack.pop();
            bound[out][1] = height.length;
            max = Math.max(max, (bound[out][1] - bound[out][0] - 1) * height[out]);
        }
        return max;
    }
}
```
