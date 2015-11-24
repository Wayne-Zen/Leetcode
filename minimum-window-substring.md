[Link](https://leetcode.com/problems/minimum-window-substring/)

```java
public class Solution {
    private boolean match(int[] a, int[] b) {
        for (int i = 0; i < 256; i++) {
            if (a[i] < b[i]) {
                return false;
            }
        }
        return true;
    }
    public String minWindow(String s, String t) {
        String res = "";
        int head = -1;
        int tail = -1;
        boolean full = false;
        int[] dict = new int[256];
        int[] observe = new int[256];
        for (int i = 0; i < t.length(); i++) {
            dict[t.charAt(i)]++;
        }
        int min = Integer.MAX_VALUE;
        
        while (true) {
            if (!full) {
                tail++;
                if (tail == s.length()) {
                    break;
                }
                char c = s.charAt(tail);
                if (dict[c] != 0) {
                    observe[c]++;
                    if (observe[c] == dict[c]) {
                        full = match(observe, dict);
                    }
                }
            } else {
                head++;
                char c = s.charAt(head);
                if (dict[c] != 0) {
                    observe[c]--;
                    if (observe[c] < dict[c]) {
                        int len = tail - head + 1;
                        if (len <= min) {
                            res = s.substring(head, tail + 1);
                            min = len;
                        }
                        full = false;
                    }
                }
            }
        }
        return res;
    }
}
```
