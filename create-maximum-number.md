[Link](https://leetcode.com/problems/create-maximum-number/)

```java
public class Solution {
    public int[] maxNumber(int[] nums1, int[] nums2, int k) {
        int[] ans = new int[k];
        for (int i = 0; i <= k; i++) {
            int cnt1 = i;
            int cnt2 = k - i;
            if (cnt1 > nums1.length || cnt2 > nums2.length) {
                continue;
            }
            int[] res1 = getMaxArray(nums1, cnt1);
            int[] res2 = getMaxArray(nums2, cnt2);
            int[] res = new int[k];
            int pos1 = 0, pos2 = 0, tpos = 0;
            // merge
            while (pos1 < res1.length || pos2 < res2.length) {
                res[tpos++] = greater(res1, pos1, res2, pos2) ? res1[pos1++] : res2[pos2++];
            }

            if (!greater(ans, 0, res, 0))
                ans = res;
        }

        return ans;
    }

    public boolean greater(int[] nums1, int start1, int[] nums2, int start2) {
        for (; start1 < nums1.length && start2 < nums2.length; start1++, start2++) {
            if (nums1[start1] > nums2[start2]) return true;
            if (nums1[start1] < nums2[start2]) return false;
        }
        return start1 != nums1.length;
    }

    
    private int[] getMaxArray(int[] array, int k) {
        int[] res = new int[k];
        int index = 0;
        for (int i = 0; i < array.length; i++) {
            int val = array[i];
            while (index > 0 && val > res[index - 1] && array.length - i >= k - index + 1) {
                index--;
            }
            if (index < k) {
                res[index++] = val;
            }
        }
        return res;
    }
}
```
