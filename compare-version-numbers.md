[Link](https://leetcode.com/problems/compare-version-numbers/)

* `.` 是regex的特殊符号

```java
public class Solution {
    public int compareVersion(String version1, String version2) {
        String[] v1 = version1.split("\\.");
        String[] v2 = version2.split("\\.");
        int i = 0;
        for (; i < Math.min(v1.length, v2.length); i++) {
            int int1 = Integer.valueOf(v1[i]);
            int int2 = Integer.valueOf(v2[i]);
            if (int1 != int2) {
                if (int1 > int2) {
                    return 1;
                } else {
                    return -1;
                }
            }
        }
        if (v1.length == v2.length) {
            return 0;
        } else if (v1.length > v2.length) {
            for (; i < v1.length; i++) {
                if (Integer.valueOf(v1[i]) != 0) {
                    return 1;
                }
            }
            return 0;
        } else {
            for (; i < v2.length; i++) {
                if (Integer.valueOf(v2[i]) != 0) {
                    return -1;
                }
            }
            return 0;
        }
    }
}
```
