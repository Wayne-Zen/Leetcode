[Link](https://leetcode.com/problems/longest-common-prefix/)

* 外层循环string， 内层循环char
* first string as target
* 检查不同string长度导致的下标越界, e.g.["hi", "hello"]

```java
public class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length == 0) {
            return "";
        }
        ArrayList<Character> res = new ArrayList<Character>();
        for (int i = 0; i < strs[0].length(); i++) {
            boolean allPass = true;
            char c = strs[0].charAt(i);
            for (int j = 1; j < strs.length; j++) {
                if (i >= strs[j].length() || strs[j].charAt(i) != c) {
                    allPass = false;
                    break;
                }
            }
            if (allPass) {
                res.add(c);
            } else {
                break;
            }
        }
        char[] res_arr = new char[res.size()];
        for (int i = 0; i < res_arr.length; i++) {
            res_arr[i] = res.get(i);
        }
        return String.valueOf(res_arr);
    }
}
```
