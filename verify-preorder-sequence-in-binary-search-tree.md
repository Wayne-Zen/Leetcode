[Link](https://leetcode.com/problems/verify-preorder-sequence-in-binary-search-tree/)

```java
public class Solution {
    public boolean verifyPreorder(int[] preorder) {
        // 维护一个递减栈
        // 出栈的序列刚好是inorder的，所以之后出栈的值只能更大
        Stack<Long> stack = new Stack<Long>();
        long min = Long.MIN_VALUE;
        for (int i = 0; i <= preorder.length; i++) {
            long x = i == preorder.length ? Long.MAX_VALUE : preorder[i];
            while (!stack.isEmpty() && x > stack.peek()) {
                long val = stack.pop();
                if (val < min) {
                    return false;
                }
                min = Math.max(min, val);
            }
            stack.push(x);
        }
        return true;
    }
}
```
