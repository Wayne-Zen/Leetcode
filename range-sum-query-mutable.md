[Link](https://leetcode.com/problems/range-sum-query-mutable/)

```java
public class NumArray {
    class TreeNode {
        int lo;
        int hi;
        int sum;
        TreeNode left;
        TreeNode right;
    }
    
    class SegmentTree {
        TreeNode root = new TreeNode();
        public void build(int[] nums) {
            root = buildHelp(nums, 0, nums.length - 1);
        }
        public TreeNode buildHelp(int[] nums, int lo, int hi) {
            TreeNode node = new TreeNode();
            node.lo = lo;
            node.hi = hi;
            if (lo == hi) {
                node.sum = nums[lo];
                return node;
            } else {
                int mid = lo + (hi - lo) / 2;
                node.left = buildHelp(nums, lo, mid);
                node.right = buildHelp(nums, mid + 1, hi);
                node.sum = node.left.sum + node.right.sum;
                return node;
            }
        }
        public void modify(int index, int val) {
            modifyHelp(root, index, val);   
        }
        public void modifyHelp(TreeNode root, int index, int val) {
            if (index < root.lo || index > root.hi) {
                return;
            }
            if (index == root.lo && index == root.hi) {
                root.sum = val;
                return;
            }
            modifyHelp(root.left, index, val);
            modifyHelp(root.right, index, val);
            root.sum = root.left.sum + root.right.sum;
        }
        public int query(int lo, int hi) {
            return queryHelp(root, lo, hi);
        }
        public int queryHelp(TreeNode root, int lo, int hi) {
            if (hi < root.lo || root.hi < lo) {
                return 0;
            }
            if (lo <= root.lo && root.hi <= hi) {
                return root.sum;
            }
            int s1 = queryHelp(root.left, lo, hi);
            int s2 = queryHelp(root.right, lo, hi);
            return s1 + s2;
        }
    }

    SegmentTree tree = new SegmentTree();
    public NumArray(int[] nums) {
        if (nums == null || nums.length == 0) {
            return;
        }
        tree.build(nums);
    }

    void update(int i, int val) {
        tree.modify(i, val);
    }

    public int sumRange(int i, int j) {
        return tree.query(i, j);
    }
}


// Your NumArray object will be instantiated and called as such:
// NumArray numArray = new NumArray(nums);
// numArray.sumRange(0, 1);
// numArray.update(1, 10);
// numArray.sumRange(1, 2);
```
