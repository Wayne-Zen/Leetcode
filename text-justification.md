[Link](https://leetcode.com/problems/text-justification/)


* 分三类情况: lineWidth + s.length() [>;==;<] maxWidth
* lineWidth 是一个词追加一个空格, 真实的lineWidth还要－1
* 注意填满maxWidth


```java
public class Solution {
    private String build(List<String> group, int maxWidth) {
        int charCnt = 0;
        for (String s : group) {
            charCnt += s.length();
        }
        int gapCnt = maxWidth - charCnt;
        StringBuilder sb = new StringBuilder();
        sb.append(group.get(0));
        for (int i = 1; i < group.size(); i++) {
            for (int k = 0; k < gapCnt / (group.size() - 1); k++) {
                sb.append(' ');
            }
            // extra space
            if (i - 1 < gapCnt % (group.size() - 1)) {
                sb.append(' ');
            }
            sb.append(group.get(i));
        }
        while (sb.length() < maxWidth) {
            sb.append(' ');
        }
        return sb.toString();
    }
    public List<String> fullJustify(String[] words, int maxWidth) {
        List<String> res = new ArrayList<String>();
        if (words == null || words.length == 0) {
            return res;
        }
        List<String> group = new ArrayList<String>();
        int len = 0; // words + one space
        for (int i = 0; i < words.length; i++) {
            String w = words[i];
            if (len + w.length() == maxWidth) {
                group.add(w);
                String line = build(group, maxWidth);
                res.add(line);
                group.clear();
                len = 0;
            } else if (len + w.length() < maxWidth) {
                group.add(w);
                len = len + w.length() + 1; // tricky
            } else if (len + w.length() > maxWidth) {
                String line = build(group, maxWidth);
                res.add(line);
                group.clear();
                len = 0;
                i--;
            }
        }
        
        // last line
        StringBuilder sb = new StringBuilder();
        if (group.size() != 0) {
            sb.append(group.get(0));
        } else {
            return res;
        }
        for (int i = 1; i < group.size(); i++) {
            sb.append(' ');
            sb.append(group.get(i));
        }
        while (sb.length() < maxWidth) {
            sb.append(' ');
        }
        res.add(sb.toString());
        return res;
    }
}
```
