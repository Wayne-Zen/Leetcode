[Link](https://leetcode.com/problems/strobogrammatic-number-iii/)

```java
public class Solution {
    public int strobogrammaticInRange(String low, String high) {
        int lowLen = low.length(), highLen = high.length(), count = 0;
        for (int i = lowLen; i <= highLen; i++) {
            if (i == lowLen || i == highLen) {
                for (String str : helper(i, i)) {                   
                    if ((i == lowLen && str.compareTo(low) < 0) || (i == highLen && str.compareTo(high) > 0))
                        continue;
                    count++;    
                }
            } else {
                count += strobogrammaticCountByLen(i);          
            }
        }
        return count;
    }

    /* 
     * For the first pair, we have 4 candidates: 1, 8, 6, 9 (excludes 0);
     * For every pair, we have 5 candidates: 0, 1, 8, 6, 9 ; 
     * For the mid of odd length, we have 3 candidates: 0, 1, 8.
     */
    int strobogrammaticCountByLen(int n) {
        int count = 0;
        if (n == 1) 
            return 3;
        if (n % 2 == 0) 
            count = 4 * (int) Math.pow(5, n / 2 - 1);       //n=even
        else 
            count = (4 * 3) * (int) Math.pow(5, n / 2 - 1); //n=odd
        return count;
    }

    public List<String> helper(int n, int len) {
        if (n == 0) return new ArrayList<String>(Arrays.asList(""));        
        if (n == 1) return new ArrayList<String>(Arrays.asList("0", "1", "8"));

        List<String> list = helper(n-2, len);
        List<String> ret = new ArrayList<String>();
        for (String s : list) {
            if (n != len) ret.add("0" + s + "0");
            ret.add("1" + s + "1");
            ret.add("8" + s + "8");
            ret.add("6" + s + "9");
            ret.add("9" + s + "6");             
        }
        return ret;
    }
}


```
