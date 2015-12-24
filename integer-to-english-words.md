[Link](https://leetcode.com/problems/integer-to-english-words/)

```java
public class Solution {
    private final String[] belowTen = new String[] {"", "One", "Two", "Three", "Four", "Five", "Six", "Seven", "Eight", "Nine"};
    private final String[] belowTwenty = new String[] {"Ten", "Eleven", "Twelve", "Thirteen", "Fourteen", "Fifteen", "Sixteen", "Seventeen", "Eighteen", "Nineteen"};
    private final String[] belowHundred = new String[] {"", "Ten", "Twenty", "Thirty", "Forty", "Fifty", "Sixty", "Seventy", "Eighty", "Ninety"};
    
    public String numberToWords(int num) {
        if (num == 0) {
            return "Zero";
        } else {
            return help(num);
        }
    }
    
    private String help(int num) {
        String res = new String();
        if (num < 10) res = belowTen[num];
        else if (num < 20) res = belowTwenty[num - 10];
        else if (num < 100) res = belowHundred[num / 10] + " " + help(num % 10);
        else if (num < 1000) res = help(num / 100)+ " Hundred " + help(num % 100);
        else if (num < 1000000) res = help(num / 1000) + " Thousand " + help(num % 1000);
        else if (num < 1000000000) res = help(num / 1000000) + " Million " + help(num % 1000000);
        else res = help(num / 1000000000) + " Billion " + help(num % 1000000000);
        return res.trim();
    }
}
```
