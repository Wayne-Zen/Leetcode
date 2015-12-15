[Link](https://leetcode.com/problems/longest-increasing-subsequence/)

```java
public class Solution {
    public int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        //dp[x] = max(dp[x], dp[y] + 1) 其中 y < x 并且 nums[x] > nums[y]
        int N = nums.length;
        int[] dp = new int[N];
        Arrays.fill(dp, 1);
        int max = 1;
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
            max = Math.max(max, dp[i]);
        }
        return max;
    }
}
```

```java
public class Solution {
    public int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        List<List<Integer>> decks = new ArrayList<List<Integer>>();
        for (int i = 0; i < nums.length; i++) {
            help(decks, nums[i]);
        }
        return decks.size();
    }
    private void help(List<List<Integer>> decks, int num) {
        if (decks.size() == 0) {
            List<Integer> deck = new ArrayList<Integer>();
            deck.add(num);
            decks.add(deck);
        } else {
            int lo = 0; 
            int hi = decks.size() - 1;
            while (lo + 1 < hi) {
                int mid = lo + (hi - lo) / 2;
                List<Integer> deck = decks.get(mid);
                int val = deck.get(deck.size() - 1);
                if (val >= num) {
                    hi = mid;
                } else {
                    lo = mid;
                }
            }
            List<Integer> deckLo = decks.get(lo);
            int valLo = deckLo.get(deckLo.size() - 1);
            List<Integer> deckHi = decks.get(hi);
            int valHi = deckHi.get(deckHi.size() - 1);
            if (valLo >= num) {
                deckLo.add(num);
            } else if (valHi >= num) {
                deckHi.add(num);
            } else {
                List<Integer> deck = new ArrayList<Integer>();
                deck.add(num);
                decks.add(deck);
            }
        }
    }
}
```
