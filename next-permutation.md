[Link](https://leetcode.com/problems/next-permutation/)

1. find dropNumber, (right to left, first decreasing number)
2. find changeNumber, (right to left, first number larger than dropNumber)
3. swap dropNumber changeNumber
4. sort region after origin dropNumber postion

![](https://lh3.googleusercontent.com/ZDrlDY3rVo61f_uQWnPTfCRsOr0rfsZS1tFqWPG6dk1CnmD3DoJU99ifqaOtEGUEIpejctPN4R6GTrgGElI2M_xJB0UEZlzMu3nt0qyrGC22wplS0zeA1NQe9Fj9N6zGkZx9DwdokOMuo3Vg2ZfScIasM5xBA4kHiTxaAot1whBU7PK9WfsVrvUzDwZthsR4tH0QBA1CslpiW-JxWUUa9J9MrruNjudk4_qOlQR2sh4UAwQBOgfQ73d0ELlh25-9EjssXwLXTR82zcxvm2cwaipTVmfWHTsj5u1m4qA02DvkvSMhXYdBBvl-iNAFLue_QBDO7iAA3Bvzs0TUu0zEJCNi7zwhiogfjusD4hbsf4q2wX3WH_dOC6JzRlmo5qA8mX-vY_9RqeuaG77jz5tXJ5Hi99v2S3xYcaFhTuVMU_uSYSQ4RbNgAlo6S3qYqFKbrDhyK-2DqKAWnk-5qY4jAabw6GlOjhMKyOQ5awpr8eIZrHlQhZa_EWcoxQlbFtOnTDkOOaeDQA9912tEikenxbKl3dS0AQMVvNmBBnYmuW4=w640-h491-no)

```java
public class Solution {
    public void nextPermutation(int[] nums) {
        
        int dropIndex = -1;
        for (int i = nums.length - 2; i >= 0; i--) {
            if (nums[i] < nums[i + 1]) {
                dropIndex = i;
                break;
            }
        }
        if (dropIndex == -1) {
            Arrays.sort(nums);
            return;
        } 
        
        int changeIndex = -1;
        for (int i = nums.length - 1; i >= 0; i--) {
            if (nums[i] > nums[dropIndex]) {
                changeIndex = i;
                break;
            }
        }
        
        swap(nums, dropIndex, changeIndex);
        Arrays.sort(nums, dropIndex + 1, nums.length);
    }
    
    private void swap(int[] nums, int x, int y) {
        int temp = nums[x];
        nums[x] = nums[y];
        nums[y] = temp;
    }
}
```
