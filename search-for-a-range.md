[Link](https://leetcode.com/problems/search-for-a-range/)

<img src="https://lh3.googleusercontent.com/UTe119WeobL-LE0eFmRwKsgnTNcooNSiqULf3kpMT3Dy0laY4T5RYRAx1a3S_K4eXKmEff5OWzM3oSMebfkybTXyIg5z1ljwd4S1lJPwUaBd8m_AXhKwpUk98fIMIpeic_PpkpbqwgNpqPUzpWvbbyEVG8WC0TcnycQ_uTgktpchEYv1LVm3hfrW9P9mZGQy6hn4WoDt0rRlJQP_xpSvWFSShtVBXsAhop3REAM9RAa6aVj3VonoAiazP6d0m9DXqJJEqyJiEDVjS-n2kORXLzaXNHcUfLCuoyvbC1UacQu_FptStjouUqUkSppvhnEvXvh2jxyysDpmJugdBFkiYa80W0WckkyyzOORm4mKbx-fzQ3d01eimRPdFP0uwfAHlfCQ8U9ELDdsFyVzeqOmj_lhfz-7REeQPVpYWP_zLLt_ZTlCgQLPIwrOtQ3VSwDbsLUu9DYt04kL0b2cmCJFsH8qf6eSXH6pnXXCTWGhLA0nQNkBbhh6-xyYempgvW5CVMND4LCg7bucdZ7rwblR_W6VmF5Al5YkO5q5oGlb0sI=w1235-h927-no" width="300">

```java
public class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] res = new int[2];
        // first nums[i] == target
        int lo = 0;
        int hi = nums.length - 1;
        while (lo + 1 < hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] < target) {
                lo = mid;
            } else {
                hi = mid;
            }
        }
        if (nums[lo] == target) {
            res[0] = lo;
        } else if (nums[hi] == target) {
            res[0] = hi;
        } else {
            return new int[]{-1, -1};
        }
        // last nums[i] == target
        lo = 0;
        hi = nums.length - 1;
        while (lo + 1 < hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] <= target) {
                lo = mid;
            } else {
                hi = mid;
            }
        }
        if (nums[hi] == target) {
            res[1] = hi;
        } else if (nums[lo] == target) {
            res[1] = lo;
        } else {
            return new int[]{-1, -1};
        }
        
        return res;
    }
}
```
