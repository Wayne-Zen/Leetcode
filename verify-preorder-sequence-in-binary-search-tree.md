[Link](https://leetcode.com/problems/verify-preorder-sequence-in-binary-search-tree/)

```java
public class Solution {
    public boolean verifyPreorder(int[] preorder) {
        // 维护一个递减栈
        // 出栈的序列刚好是inorder的，所以之后出栈的值只能更大
        Stack<Integer> stack = new Stack<Integer>();
        int low = Integer.MIN_VALUE;
        for (int x : preorder) {
            if (x < low) {
                return false;
            }
            if (stack.isEmpty() || stack.peek() > x) {
                stack.push(x);
                continue;
            }
            while (!stack.isEmpty() && stack.peek() < x) {
                int val = stack.pop();
                low = Math.max(low, val);
            }
            stack.push(x);
        }
        return true;
    }
}
```
