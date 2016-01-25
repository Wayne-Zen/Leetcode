[Link](https://leetcode.com/problems/number-of-digit-one/)

* 由低位向高位依次遍历数字n的每一位curn
* 记当前位数为c，curn左边（高位）的数字片段为highn，cur右边（低位）的数字片段为lown，lowc = 10 ^ c
* 若curn = 0，则高位范围为0 ~ highn - 1，低位0 ~ lowc - 1
* 若curn = 1，则高位范围为0 ~ highn - 1，低位0 ~ lowc - 1；或者 高位为highn， 低位0 ~ lown
* 若curn ＞ 1，则高位范围为0 ~ highn， 低位为0 ~ lowc - 1


```java
public class Solution {
    public int countDigitOne(int n) {
        int res = 0;
        int curn = 0;
        int lown = 0;
        int highn = n;
        int lowc = 1;
        while (highn > 0) {
            curn = highn % 10;
            highn = highn / 10;
            if (curn == 1) {
                res += highn * lowc;
                res += lown + 1;
            } else if (curn < 1) {
                res += highn * lowc;
            } else if (curn > 1) {
                res += (highn + 1) * lowc;
            }
            lown = lown + lowc * curn;
            lowc *= 10;
        }
        return res;
    }
}
```
