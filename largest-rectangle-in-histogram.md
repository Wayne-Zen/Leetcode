[Link](https://leetcode.com/problems/largest-rectangle-in-histogram/)

* 一定要记住入站

```java
public class Solution {
    public int largestRectangleArea(int[] height) {
        // store index
        Stack<Integer> stack = new Stack<Integer>();
        int[][] bound = new int[height.length][2];
        int max = 0;
        for (int in = 0; in < height.length; in++) {
            while (!stack.isEmpty() 
                    && height[stack.peek()] >= height[in]) {
                int out = stack.pop();
                bound[out][1] = in;
                //出战时，两边bound肯定都有了
                int area = height[out] * (bound[out][1] - bound[out][0] - 1);
                max = Math.max(max, area);
            }
            if (stack.isEmpty()) {
                bound[in][0] = -1;
            } else { // height[stack.peek()] < height[in]
                bound[in][0] = stack.peek();
            }
            stack.push(in); // 无论如何都要入站
        }
        while (!stack.isEmpty()) {
            int out = stack.pop();
            bound[out][1] = height.length;
            int area = height[out] * (bound[out][1] - bound[out][0] - 1);
            max = Math.max(max, area);
        }
        return max;
    }
}
```
