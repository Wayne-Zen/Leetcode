[Link](https://leetcode.com/problems/excel-sheet-column-title/)

* 非常像，但是不完全等价于10进制转26进制，没有字母表示当前位为0
* 注意使用 `n － 1`

```java
public class Solution {
    public String convertToTitle(int n) {
        StringBuilder sb = new StringBuilder();
        while (n > 0) {
            sb.insert(0, (char)('A' + (n - 1) % 26));
            n = (n - 1) / 26;
        }
        return sb.toString();
    }
}
```
