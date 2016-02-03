[Link](https://leetcode.com/problems/count-of-range-sum/)

The merge sort based solution counts the answer while doing the merge. During the merge stage, we have already sorted the left half `[start, mid)` and right half `[mid, end)`. We then iterate through the left half with index `i`. For each `i`, we need to find two indices `k` and `j` in the right half where

* `j` is the first index satisfy `S_j - S_i > upper`;
* `k` is the first index satisfy `S_k - S_i >= lower`.

Then the number of sums in `[lower, upper]` is `j-k`. We also use another index `t` to copy the elements satisfy `S_t < S_i` to a cache in order to complete the merge sort.

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

```java
public class Solution {
    public int countRangeSum(int[] nums, int lower, int upper) {
        int n = nums.length;
        long[] sums = new long[n + 1];
        for (int i = 1; i <= n; i++)
            sums[i] = sums[i - 1] + nums[i - 1];
        return help(sums, 0, n, lower, upper); 
    }
    
    private int help(long[] sums, int lo, int hi, int lower, int upper) {
        if (lo == hi) {
            return 0;
        }
        int mid = lo + (hi - lo) / 2;
        int cnt = help(sums, lo, mid, lower, upper)
                + help(sums, mid + 1, hi, lower, upper);
        // count
        int p1 = mid + 1;
        int p2 = mid + 1;
        for (int i = lo; i <= mid; i++) {
            while (p1 <= hi && sums[p1] - sums[i] < lower) {
                p1++;
            }
            while (p2 <= hi && sums[p2] - sums[i] <= upper) {
                p2++;
            }
            cnt += p2 - p1;
        }
        // sort
        long[] cache = new long[hi - lo + 1];
        int h1 = lo;
        int h2 = mid + 1;
        int index = 0;
        while (h1 <= mid && h2 <= hi) {
            if (sums[h1] < sums[h2]) {
                cache[index++] = sums[h1++];
            } else {
                cache[index++] = sums[h2++];
            }
        }
        while (h1 <= mid) {
            cache[index++] = sums[h1++];
        }
        while (h2 <= hi) {
            cache[index++] = sums[h2++];
        }
        index = 0;
        for (int i = lo; i <= hi; i++) {
            sums[i] = cache[index++];
        }
        return cnt;
    }
}
```
