[Link](https://leetcode.com/problems/count-of-range-sum/)

```java
public class Solution {
    class TreeNode {
        long val;
        int leftCnt; // number of node in left sub tree <=
        int rightCnt; // number of node in right sub tree >
        TreeNode left;
        TreeNode right;
        public TreeNode(long val) {
            this.val = val;
        }
    }
    public int countRangeSum(int[] nums, int lower, int upper) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int n = nums.length;
        long[] sums = new long[n + 1];
        for (int i = 0; i < n; ++i) {
            sums[i + 1] = sums[i] + nums[i];
        }
        TreeNode root = new TreeNode(sums[sums.length - 1]);
        int res = 0;
        for (int i = sums.length - 2; i >= 0; i--) {
            res += insert(root, sums[i], lower, upper);
        }
        return res;
    }
    private int insert(TreeNode root, long val, int lower, int upper) {
        int res = root.leftCnt + root.rightCnt + 1;
        TreeNode move = root;
        while (move != null) {
            if (move.val - val > upper) {
                res -= move.rightCnt + 1;
                move = move.left;
            } else {
                move = move.right;
            }
        }
        move = root;
        while (move != null) {
            if (move.val - val < lower) {
                res -= move.leftCnt + 1;
                move = move.right;
            } else {
                move = move.left;
            }
        }
        while (true) {
            if (val <= root.val) {
                root.leftCnt++;
                if (root.left == null) {
                    root.left = new TreeNode(val);
                    break;
                } else {
                    root = root.left;
                }
            } else {
                root.rightCnt++;
                if (root.right == null) {
                    root.right = new TreeNode(val);
                    break;
                } else {
                    root = root.right;
                }
            }
        }
        return res;
    }
}
```

```java
public class Solution {
    public int countRangeSum(int[] nums, int lower, int upper) {
        int n = nums.length;
        long[] sums = new long[n + 1];
        for (int i = 0; i < n; ++i)
            sums[i + 1] = sums[i] + nums[i];
        return countWhileMergeSort(sums, 0, n + 1, lower, upper);
    }
    
    private int countWhileMergeSort(long[] sums, int start, int end, int lower, int upper) {
        if (end - start <= 1) return 0;
        int mid = (start + end) / 2;
        int count = countWhileMergeSort(sums, start, mid, lower, upper) 
                  + countWhileMergeSort(sums, mid, end, lower, upper);
        int j = mid, k = mid, t = mid;
        long[] cache = new long[end - start];
        for (int i = start, r = 0; i < mid; ++i, ++r) {
            while (k < end && sums[k] - sums[i] < lower) k++;
            while (j < end && sums[j] - sums[i] <= upper) j++;
            while (t < end && sums[t] < sums[i]) cache[r++] = sums[t++];
            cache[r] = sums[i];
            count += j - k;
        }
        System.arraycopy(cache, 0, sums, start, t - start);
        return count;
    }
}
```
