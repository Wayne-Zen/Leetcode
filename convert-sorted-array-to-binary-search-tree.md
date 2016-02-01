[Link](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)

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
    public TreeNode sortedArrayToBST(int[] nums) {
        if (nums == null || nums.length == 0) {
            return null;
        }
        return help(nums, 0, nums.length - 1);
    }
    private TreeNode help(int[] nums, int lo, int hi) {
        if (lo > hi) {
            return null;
        }
        int mid = lo + (hi - lo) / 2;
        TreeNode root = new TreeNode(nums[mid]);
        root.left = help(nums, lo, mid - 1);
        root.right = help(nums, mid + 1, hi);
        return root;
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
    int index = 0;
    public TreeNode sortedArrayToBST(int[] nums) {
        return help(nums, nums.length);
    }
    public TreeNode help(int[] nums, int size) {
        if (size <= 0) {
            return null;
        }
        TreeNode left = help(nums, size / 2);
        TreeNode root = new TreeNode(nums[index++]);
        TreeNode right = help(nums, size - size / 2 - 1);
        root.left = left;
        root.right = right;
        return root;
    }
}
```
