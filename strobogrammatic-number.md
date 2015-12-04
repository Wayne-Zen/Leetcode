[Link](https://leetcode.com/problems/strobogrammatic-number/)

```java
public class Solution {
    public boolean isStrobogrammatic(String num) {
        HashMap<Character, Character> map = new HashMap<Character, Character>();
        map.put('6', '9');
        map.put('9', '6');
        map.put('1', '1');
        map.put('8', '8');
        map.put('0', '0');
        int head = 0;
        int tail = num.length() - 1;
        while (head <= tail) {
            char c1 = num.charAt(head);
            char c2 = num.charAt(tail);
            if (!map.containsKey(c1) || !map.get(c1).equals(c2)) {
                return false;
            } else {
                head++;
                tail--;
            }
        }
        return true;
    }
}
```
