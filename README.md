# Leetcode


* [Integer to Roman](https://github.com/Wayne-Zen/Leetcode/blob/master/integer-to-roman.md)
* [Roman to Integer](https://github.com/Wayne-Zen/Leetcode/blob/master/roman-to-integer.md)
* [Integer to English Words](https://github.com/Wayne-Zen/Leetcode/blob/master/integer-to-english-words.md)
* [Divide Two Integers](https://github.com/Wayne-Zen/Leetcode/blob/master/divide-two-integers.md)
* [Fraction to Recurring Decimal](https://github.com/Wayne-Zen/Leetcode/blob/master/fraction-to-recurring-decimal.md)
* [Word Break II](https://github.com/Wayne-Zen/Leetcode/blob/master/word-break-ii.md)
* [Convert Sorted List to Binary Search Tree](https://github.com/Wayne-Zen/Leetcode/blob/master/convert-sorted-list-to-binary-search-tree.md)
* [Valid Number](https://github.com/Wayne-Zen/Leetcode/blob/master/valid-number.md)
* [String to Integer (atoi)](https://github.com/Wayne-Zen/Leetcode/blob/master/string-to-integer-atoi.md)


```java

public class Solution {
    /**
     * @param pages: an array of integers
     * @param k: an integer
     * @return: an integer
     */
    public int copyBooks(int[] pages, int k) {
        if (pages == null || pages.length == 0) {
            return -1;
        }
        // m books->row, k workers->col
        int m = pages.length;
        // running sum, page sum of first i book
        int[] sum = new int[m + 1];
        for (int i = 1; i <= m; i++) {
            sum[i] = sum[i - 1] + pages[i - 1];
        }
        // assign copy first i books to first j worker
        int[][] dp = new int[m + 1][k + 1];
        for (int i = 1; i <= m; i++) {
            // only one worker
            dp[i][1] = sum[i];
            for (int j = 2; j <= k; j++) {
                int min = Integer.MAX_VALUE;
                for (int x = 1; x <= i; x++) {
                    // jth people copy start from xth book, (copy at leat one book, at most all books)
                    int temp = Math.max(dp[x - 1][j - 1], sum[i] - sum[x - 1]);
                    if (temp < min) {
                        min = temp;
                        dp[i][j] = min;
                    }
                }
            }
        }
        return dp[m][k];
    }
}



public class Solution {
    /**
     * @param pages: an array of integers
     * @param k: an integer
     * @return: an integer
     */
    public int copyBooks(int[] pages, int k) {
        if (pages == null || pages.length == 0) {
            return -1;
        }
        // m books->row, k workers->col
        int m = pages.length;
        int max = 0;
        for (int page : pages) {
            max = Math.max(max, page);
        }
        if (k >= m) {
            return max;
        }
        // running sum, page sum of first i book
        int[] sum = new int[m + 1];
        for (int i = 1; i <= m; i++) {
            sum[i] = sum[i - 1] + pages[i - 1];
        }
        // assign copy first i books to first j worker
        int[][] dp = new int[m + 1][k + 1];
        // store x value that give dp solution
        // s[i - 1][j] <= s[i][j] <= s[i + 1][j]
        // s[i][j - 1] <= s[i][j] <= s[i][j + 1]
        // s 比 dp 多一列, 假设多一个worker, 可以再初始化时确定值，用作bound
        int[][] s = new int[m + 1][k + 2];
        for (int i = 1; i <= m; i++) {
            // only one worker
            dp[i][1] = sum[i];
            s[i][1] = 1;
            s[i][Math.min(i, k + 1)] = i;
            for (int j = Math.min(i, k + 1) - 1; j >= 2; j--) {
                int min = Integer.MAX_VALUE;
                for (int x = s[i][j + 1]; x >= s[i - 1][j]; x--) {
                    // jth people copy start from xth book, (copy at leat one book, at most all books)
                    int temp = Math.max(dp[x - 1][j - 1], sum[i] - sum[x - 1]);
                    if (temp < min) {
                        min = temp;
                        dp[i][j] = min;
                        s[i][j] = x;
                    }
                }
            }
        }
        return dp[m][k];
    }
}
```
