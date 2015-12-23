[Link](https://leetcode.com/problems/h-index/)

```java
public class Solution {
    public int hIndex(int[] citations) {
        int N = citations.length;
        int[] cnt = new int[N + 1];
        for (int cite : citations) {
            if (cite >= N) {
                cnt[N]++;
            } else {
                cnt[cite]++;
            }
        }
        int sum = 0;
        for (int i = N; i >= 0; i--) {
            sum += cnt[i];
            if (sum >= i) {
                return i;
            }
        }
        return 0;
    }
}
```
