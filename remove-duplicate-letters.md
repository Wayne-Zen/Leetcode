[Link](https://leetcode.com/problems/remove-duplicate-letters/)

```java
public class Solution {
    public String removeDuplicateLetters(String s) {
        if (s == null || s.length() == 0) {
            return "";
        }  
        int[] cnt = new int[26];
        for (char c : s.toCharArray()) {
            cnt[c - 'a']++;
        }
        Stack<Character> stack = new Stack<Character>();
        HashSet<Character> set = new HashSet<Character>();
        for (char c : s.toCharArray()) {
            cnt[c - 'a']--;
            if (set.contains(c)) {
                continue;
            }
            while (!stack.isEmpty() && c < stack.peek() && cnt[stack.peek() - 'a'] != 0) {
                set.remove(stack.pop());
            }
            stack.push(c);
            set.add(c);
        }
        StringBuilder sb = new StringBuilder();
        while (!stack.isEmpty()) {
            sb.append(stack.pop());
        }
        return sb.reverse().toString();
    }
}
```
