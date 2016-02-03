[Link](https://leetcode.com/problems/number-of-digit-one/)

* 由低位向高位依次遍历数字n的每一位curn
* 记当前位数为c，curn左边（高位）的数字片段为highn，cur右边（低位）的数字片段为lown，lowc = 10 ^ c
* 若curn = 0，则高位范围为0 ~ highn - 1，低位0 ~ lowc - 1
* 若curn = 1，则高位范围为0 ~ highn - 1，低位0 ~ lowc - 1；或者 高位为highn， 低位0 ~ lown
* 若curn ＞ 1，则高位范围为0 ~ highn， 低位为0 ~ lowc - 1


```java
public class Solution {
    public int countDigitOne(int n) {
        if (n <= 0) {
            return 0;
        }
        int lown = 0; // low part number;
        int lowc = 1; // 10^(lown.length)
        int highn = n / 10; // high part number; 
        int now = n % 10;  // current digit;
        int cnt = 0;
        while (lown != n) {
            if (now == 1) {
                //     [highn, highn] & [0, lown]
                cnt += lown + 1;
                //     [0, highn - 1] & [0, 99...]
                cnt += highn * lowc;
            } else if (now > 1) {
                //     [0, highn] & [0, 99...]
                cnt += (highn + 1) * lowc;
            } else if (now < 1) {
                //     [0, hignn - 1] & [0, 99...]
                cnt += highn * lowc;
            }
            lown = lowc * now + lown;
            now = highn % 10;
            highn /= 10;
            lowc *= 10;
        }
        return cnt;
    }
}
```
