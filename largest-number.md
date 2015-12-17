[Link](https://leetcode.com/problems/largest-number/)

```java
public class Solution {
    public String largestNumber(int[] nums) {
        ArrayList<Integer> list = new ArrayList<Integer>();
        for (int num: nums) {
            list.add(num);
        }
        Collections.sort(list, new Comparator<Integer>() {
            public int compare(Integer i1, Integer i2) {
                return ("" + i2 + i1).compareTo("" + i1 + i2);
            }
        });
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < list.size(); i++) {
            sb.append(list.get(i));
        }
        if (sb.charAt(0) == '0') {
            return "0";
        }
        return sb.toString();
    }
}
```
