[Link](https://leetcode.com/problems/inorder-successor-in-bst/)

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public TreeNode inorderSuccessor(TreeNode root, TreeNode p) {
        Stack<TreeNode> stk = new Stack<TreeNode>();
        TreeNode curr = root;
        // 找到目标节点并把路径上的节点压入栈
        while(curr != p){
            stk.push(curr);
            if(curr.val > p.val){
                curr = curr.left;
            } else {
                curr = curr.right;
            }
        }
        // 如果目标节点有右节点，则找到其右节点的最左边的节点，就是下一个数
        if(curr.right != null){
            curr = curr.right;
            while(curr.left != null){
                curr = curr.left;
            }
            return curr;
        } else {
        // 如果没有右节点，pop栈找到第一个比目标节点大的节点
            while(!stk.isEmpty() && stk.peek().val < curr.val){
                stk.pop();
            }
            // 如果栈都pop空了还没有比目标节点大的，说明没有更大的了
            return stk.isEmpty() ? null : stk.pop();
        }
    }
}
```
