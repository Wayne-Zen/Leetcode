[Link](https://leetcode.com/problems/happy-number/)

```java
public class Solution {
    public boolean isHappy(int n) {
        int newN = 0;
        HashSet<Integer> set = new HashSet<Integer>();

        while(!set.contains(n)){
            set.add(n);
            newN = 0;
            while(n != 0){
                newN += (n % 10) * (n % 10);
                n /= 10;
            }
            n = newN;

            if(n == 1) return true;
        }

        return false;
    }
}
```
