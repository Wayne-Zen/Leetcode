[Link](https://leetcode.com/problems/recover-binary-search-tree/)

* 如果是中序遍历相邻的两个元素被调换了，很容易想到就只需会出现一次违反情况，只需要把这个两个节点记录下来最后调换值就可以；
* 如果是不相邻的两个元素被调换了，举个例子很容易可以发现，会发生两次逆序的情况，那么这时候需要调换的元素应该是第一次逆序前面的元素，和第二次逆序后面的元素。
* 比如1234567,1和5调换了，会得到5234167，逆序发生在52和41，我们需要把4和1调过来，那么就是52的第一个元素，41的第二个元素调换即可。
* 可以看到实现中pre用了一个ArrayList来存，这样做的原因是因为java都是值传递

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
    public void recoverTree(TreeNode root) {
        ArrayList<TreeNode> prev = new ArrayList<TreeNode>();
        prev.add(null);
        ArrayList<TreeNode> swap = new ArrayList<TreeNode>();
        help(prev, root, swap);
        if (swap.size() > 0) {
            int temp = swap.get(0).val;
            swap.get(0).val = swap.get(1).val;
            swap.get(1).val = temp;
        }
    }
    private void help(ArrayList<TreeNode> prev,
                      TreeNode root,
                      ArrayList<TreeNode> swap) {
        if (root == null) {
            return;
        }    
        help(prev, root.left, swap);
        if (prev.get(0) != null && prev.get(0).val > root.val) {
            if (swap.size() == 0) {
                swap.add(prev.get(0));
                swap.add(root);
            } else {
                swap.set(1, root);
            }
        }
        prev.set(0, root);
        help(prev, root.right, swap);
    }
}
```

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
    public void recoverTree(TreeNode root) {
        if (root == null) {
            return;
        }
        Stack<TreeNode> stack = new Stack<TreeNode>();
        
        while (root != null) {
            stack.push(root);
            root = root.left;
        }
        TreeNode prev = new TreeNode(Integer.MIN_VALUE);
        List<TreeNode[]> swaps = new ArrayList<TreeNode[]>();
        while (!stack.isEmpty()) {
            root = stack.pop();
            if (prev.val > root.val) {
                TreeNode[] swap = new TreeNode[2];
                swap[0] = prev;
                swap[1] = root;
                swaps.add(swap);
            }
            prev = root;
            root = root.right;
            while (root != null) {
                stack.push(root);
                root = root.left;
            }
        }
        
        if (swaps.size() == 1) {
            TreeNode[] swap = swaps.get(0);
            swapNodeVal(swap[0], swap[1]);
        } else {
            TreeNode[] swap0 = swaps.get(0);
            TreeNode[] swap1 = swaps.get(1);
            swapNodeVal(swap0[0], swap1[1]);
        }
    }
    private void swapNodeVal(TreeNode n1, TreeNode n2) {
        int temp = n1.val;
        n1.val = n2.val;
        n2.val = temp;
    }
}
```
