[Link](https://leetcode.com/problems/fraction-to-recurring-decimal/)

```java
public class Solution {
    public String fractionToDecimal(int numerator, int denominator) {
        if (numerator == 0) return "0";
        if (denominator == 0) return "";
        StringBuilder sb = new StringBuilder();
        if ((numerator > 0) != (denominator > 0)) {
            sb.append('-');
        }
        long num = Math.abs((long)numerator);
        long den = Math.abs((long)denominator);
        sb.append(num / den);
        long rem = (num % den) * 10;
        if (rem == 0) {
            return sb.toString();
        }
        sb.append('.');
        HashMap<Long, Integer> map = new HashMap<Long, Integer>();
        while (rem != 0) {
            if (map.containsKey(rem)) {
                int loc = map.get(rem);
                return sb.substring(0, loc) + "(" + sb.substring(loc) + ")";
            }
            map.put(rem, sb.length());
            sb.append(rem / den);
            rem = (rem % den) * 10;
        }
        return sb.toString();
    }
}
```
