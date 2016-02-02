[Link](http://www.lintcode.com/en/problem/copy-books/)

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
        int N = pages.length;
        int sum = 0;
        int max = 0;
        for (int page : pages) {
            sum += page;
            max = Math.max(max, page);
        }
        int lo = max;
        int hi = sum;
        while (lo + 1 < hi) {
            int mid = lo + (hi - lo) / 2;
            int workerNum = assign(pages, mid);
            System.err.println(workerNum);
            if (workerNum > k)  {
                lo = mid; // quota too low, workerNum too high, increase quota
            } else if (workerNum < k) {
                hi = mid; // decrease quota
            } else if (workerNum == k) {
                hi = mid; // try to get min quota
            }
        }
        if (assign(pages, lo) <= k) {
            return lo;
        } else {
            return hi;
        }
    }
    
    private int assign(int[] pages, int quota) {
        System.err.println(quota);
        int workerNum = 1;
        int load = 0;
        for (int i = 0; i < pages.length; i++) {
            if (load + pages[i] <= quota) {
                load += pages[i];
            } else {
                // next worker
                load = pages[i];
                workerNum++;
            }
        }
        return workerNum;
    }
}
```


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
```


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
