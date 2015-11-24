[Link](https://leetcode.com/problems/text-justification/)


* 分三类情况: lineWidth + s.length() [>;==;<] maxWidth
* lineWidth 是一个词追加一个空格, 真实的lineWidth还要－1
* 注意填满maxWidth


```java
public class Solution {
    private String buildFull(ArrayList<String> sub, int maxWidth) {
        StringBuilder sb = new StringBuilder();
        sb.append(sub.get(0));
        for (int i = 1; i < sub.size(); i++) {
            sb.append(' ');
            sb.append(sub.get(i));
        }
        // 坑
        while (sb.length() != maxWidth) {
            sb.append(' ');
        }
        return sb.toString();
    }
    
    private String buildGap(ArrayList<String> sub, int maxWidth, int lineWidth) {
        int gap = maxWidth - lineWidth;
        int interval = sub.size() - 1;
        int[] spaceCnt = new int[interval];
        for (int i = 0; i < interval; i++) {
            spaceCnt[i] = 1 + gap / interval;
            if (i < gap % interval) {
                spaceCnt[i]++;
            }
        }
        StringBuilder sb = new StringBuilder();
        sb.append(sub.get(0));
        for (int i = 1; i < sub.size(); i++) {
            for (int j = 0; j < spaceCnt[i - 1]; j++) {
                sb.append(' ');
            }
            sb.append(sub.get(i));
        }
        while (sb.length() != maxWidth) {
            sb.append(' ');
        }
        return sb.toString();
    } 
    
    public List<String> fullJustify(String[] words, int maxWidth) {
        List<String> res = new ArrayList<String>();
        if (words == null || words.length == 0) {
            return res;
        }
        int lineWidth = 0;
        ArrayList<String> sub = new ArrayList<String>();
        for (int i = 0; i < words.length; i++) {
            String s = words[i];
            if (s.length() > maxWidth) {
                throw new IllegalArgumentException();
            }
            if (lineWidth + s.length() == maxWidth) {
                sub.add(s);
                res.add(buildFull(sub, maxWidth));
                lineWidth = 0;
                sub.clear();
            } else if (lineWidth + s.length() < maxWidth) {
                sub.add(s);
                lineWidth = lineWidth + s.length() + 1;
            } else if (lineWidth + s.length() > maxWidth) {
                res.add(buildGap(sub, maxWidth, lineWidth - 1)); // 坑
                lineWidth = 0;
                sub.clear();
                i--;
            }
        }
        if (!sub.isEmpty()) {
            res.add(buildFull(sub, maxWidth));
        }
        return res;
    }
}
```
