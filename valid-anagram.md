[Link](https://leetcode.com/problems/valid-anagram/)

```java
public class Solution {
    public boolean isAnagram(String s, String t) {
        int[] dict = new int[256];
        for (char c : s.toCharArray()) {
            dict[c]++;
        }
        for (char c : t.toCharArray()) {
            dict[c]--;
        }
        for (int i = 0; i < 256; i++) {
            if (dict[i] != 0) {
                return false;
            }
        }
        return true;
    }
}
```
