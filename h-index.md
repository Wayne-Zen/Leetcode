[Link](https://leetcode.com/problems/h-index/)

O(n)

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
        int h = 0;
        for (int i = N; i >= 0; i--) {
            sum += cnt[i];
            int currH = Math.min(sum, i);
            if (currH >= h) {
                h = currH;
            } else {
                return h;
            }
        }
        return h;
    }
}
```

O(nlogn)
```java
public class Solution {
    public int hIndex(int[] citations) {
        // 排序
        Arrays.sort(citations);
        int h = 0;
        for(int i = 0; i < citations.length; i++){
            // 得到当前的H指数
            int currH = Math.min(citations.length - i, citations[i]);
            if(currH >= h){
                h = currH;
            } else {
                return h;
            }
        }
        return h;
    }
}
```
