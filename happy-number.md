[Link](https://leetcode.com/problems/happy-number/)

```java
public class Solution {
    public boolean isHappy(int n) {
        HashSet<Integer> set = new HashSet<Integer>();
        
        while (true) {
            int newN = 0;
            while (n > 0) {
                newN += (n % 10) * (n % 10);
                n = n / 10;
            }
            n = newN;
            if (n == 1) {
                return true;
            }
            if (set.contains(n)) {
                return false;
            } else {
                set.add(n);
            }
        }
    }
}
```
