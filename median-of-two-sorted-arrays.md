[Link](https://leetcode.com/problems/median-of-two-sorted-arrays/)

* 找第k个数， 每次干掉k/2个数
* consider the tail of A or B as positive infinity
* all the index involes start index
* 结束条件
    1. startA >= A.length
    2. startB >= B.length
    3. k == 1

```java
public class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int m = nums1.length;
        int n = nums2.length;
        int sum = m + n;
        if (sum % 2 == 1) {
            return (double)getKth(nums1, 0, nums2, 0, sum/2 + 1);
        } else {
            return (getKth(nums1, 0, nums2, 0, sum/2) 
                    + getKth(nums1, 0, nums2, 0, sum/2 + 1)) / 2.0;
        }
    }
    
    private int getKth(int[] A, int startA, int[] B, int startB, int k) {
        while (!(k == 1 || startA == A.length || startB == B.length)) {
            int keyA = startA + k/2 - 1 < A.length 
                       ? A[startA + k/2 - 1] 
                       : Integer.MAX_VALUE;
            int keyB = startB + k/2 - 1 < B.length 
                       ? B[startB + k/2 - 1] 
                       : Integer.MAX_VALUE;
            
            if (keyA >= keyB) {
                startB = k/2 + startB;
            } else {
                startA = k/2 + startA;
            }
            k = k - k/2;
        }
        if (startA == A.length) {
            return B[startB + k - 1];
        }
        if (startB == B.length) {
            return A[startA + k - 1];
        }
        if (k == 1) {
            return Math.min(A[startA], B[startB]);
        }
        return 0;
    }
}
```
