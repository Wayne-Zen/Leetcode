[Link](https://leetcode.com/problems/flip-game-ii/)

```java
public class Solution {
    public boolean canWin(String s) {
        for (int i = 0; i < s.length() - 1; ++i)
            if (s.charAt(i) == '+' && s.charAt(i + 1) == '+' && !canWin(s.substring(0, i) + "--" + s.substring(i + 2)))
                    return true;
        return false;
    }
}
```
