[Link](https://leetcode.com/problems/container-with-most-water/)

<img src="https://lh3.googleusercontent.com/8dtJOsq8041hQWEFwElVtRQDfaov75v3fyGzL5McjXQ6FSyliBGYNrp5BRTxqwn86EnDbBaSGLniDeq_Fhwad8jJGHFRAbD0UPovPHswr1YN5k3LALDRamWpGENzMixerJdgjUc112JvaDr_lRWwYZLkfIpe-EMRpV6CHfBNXxFHPlQiOoVVp0Ad3q5AmsSX6gfnr1rUKmoo7Rixw3yTjfBGoXJFTx3Kzjbfma87ZcF7fFJ0aX7HcXQBNBXIZxJsM0b7REum8qJ3XTU5bzJP2mdvJTVNUn5vUE07D3sCItJfQelQVXh0rf8w6R9UaX8fTbyqB3VS-YBCB3VD8juXBl0IUgGkvlc56vsF0v-XZDq5xQM66-O27Cym7yrUSVlPHugKnrYTPWIuDQsmTeltWckHSQXqBg3wsuPcqpPS458q2SpDYrA39xJX4TSaKjDC-Ck_uRBWavGUrin2axnXwlpxINO7B7xtX6shvnyKls42Lx4ckDdWP3x4KeOuxm-yQm-lNQBL9QrLsIxPe8Za-pCT90738VBSOf1L_fSIPt0=w713-h261-no" width="600">

* 假定初始的盛水面积为ans=0，lh为左边的高度，rh为右边的高度，如果lh < rh, 则向右运动，寻找第一个比当前lh大的左节点。同理，如果lh > rh，则向左运动，寻找第一个比当前rh大的右节点。

```java
public class Solution {
    public int maxArea(int[] height) {
        
        int lpos = 0;
        int rpos = height.length - 1;
        int max = 0;
        
        while (lpos < rpos) {
            int area =  Math.min(height[lpos], height[rpos]) * (rpos - lpos);
            max = Math.max(max, area);
            if (height[lpos] < height[rpos]) {
                lpos++;
            } else {
                rpos--;
            }
        }
        
        return max;
    }
}
```
