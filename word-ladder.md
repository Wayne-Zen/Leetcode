[Link](https://leetcode.com/problems/word-ladder/)

* 需要一个HashSet纪录visited，避免走回头路。

```java
public class Solution {
    public int ladderLength(String beginWord, String endWord, Set<String> wordList) {
        if (!wordList.contains(beginWord) || !wordList.contains(endWord)) {
            return 0;
        }
        if (beginWord.length() != endWord.length()) {
            return 0;
        }
        int len = 0;
        HashSet<String> visited = new HashSet<String>();
        LinkedList<String> queue = new LinkedList<String>();
        queue.offer(beginWord);
        visited.add(beginWord);
        while (!queue.isEmpty()) {
            len++;
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                String s = queue.poll();
                if (s.equals(endWord)) {
                    return len;
                }
                List<String> next = getNext(s, wordList);
                for (String n : next) {
                    if (visited.contains(n)) {
                        continue;
                    }
                    visited.add(n);
                    queue.offer(n);
                }
            }
        }
        return 0;
    }
    private List<String> getNext(String s, Set<String> wordList) {
        List<String> res = new ArrayList<String>();
        char[] arr = s.toCharArray();
        for (int i = 0; i < s.length(); i++) {
            char origin = arr[i];
            for (char c = 'a'; c <= 'z'; c++) {
                arr[i] = c;
                String change = new String(arr);
                if (wordList.contains(change)) {
                    res.add(change);
                }
            }
            arr[i] = origin;
        }
        return res;
    }
}
```
