[Link](https://leetcode.com/problems/verify-preorder-serialization-of-a-binary-tree/)

```java
public class Solution {
    public boolean isValidSerialization(String preorder) {
        String[] vals = preorder.split(",");
        Stack<TreeNode> stack = new Stack<TreeNode>();
        stack.push(new TreeNode(-1));
        int index = 0;
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            if (index == vals.length) {
                return false;
            }
            if (!vals[index].equals("#")) {
                stack.push(new TreeNode(-1)); // right
                stack.push(new TreeNode(-1)); // left
            }
            index++;
        }
        return index == vals.length;
    }
}
```
```java
public class Solution {
    int index = 0;
    public boolean isValidSerialization(String preorder) {
        String[] vals = preorder.split(",");
        index = 0;
        if (help(vals)) {
            return index == vals.length;
        } else {
            return false;
        }
    }
    private boolean help(String[] vals) {
        if (index == vals.length) {
            return false;
        }
        String val = vals[index++];
        if (val.equals("#")) {
            return true;
        } else{
            boolean left = help(vals);
            boolean right = help(vals);
            return left && right;
        }
    }
}
```
