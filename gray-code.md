[Link](https://leetcode.com/problems/gray-code/)

* n = 0; [0]
* n = 1; [0,1];
* 原序前面加0，逆序前面加1

```java
public class Solution {
    public List<Integer> grayCode(int n) {
        List<Integer> res = new LinkedList<Integer>();
        if (n == 0) {
            res.add(0);
            return res;
        }
        if (n == 1) {
            res.add(0);
            res.add(1);
            return res;
        }
        List<Integer> base = grayCode(n - 1);
        for (int i : base) {
            res.add(i);
        }
        for (int i = base.size() - 1; i >= 0; i--) {
            res.add((1 << (n - 1)) + base.get(i));
        }
        
        return res;
    }
}
```
