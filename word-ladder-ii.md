[Link](https://leetcode.com/problems/word-ladder-ii/)

* 先bfs，后dfs
* dist 是关键

```java
public class Solution {
    private List<String> getNextWords(String s, Set<String> wordList, 
                                      HashMap<String, List<String>> next) {
        if (next.containsKey(s)) {
            return next.get(s);
        }
        List<String> res = new ArrayList<String>();
        char[] arr = s.toCharArray();
        for (int i = 0; i < s.length(); i++) {
            char origin = arr[i];
            for (char c = 'a'; c <= 'z'; c++) {
                arr[i] = c;
                String w = new String(arr);
                if (wordList.contains(w)) {
                    res.add(w);
                }
            }
            arr[i] = origin;
        }
        next.put(s, res);
        return res;
    }
    
    private void help(List<List<String>> res,
                      List<String> now,
                      HashMap<String, Integer> dist,
                      HashMap<String, List<String>> next,
                      Set<String> wordList,
                      String target) {
        String current = now.get(now.size() - 1);
        if (current.equals(target)) {
            List<String> cp = new ArrayList<String>(now);
            Collections.reverse(cp);
            res.add(cp);
            return;
        }
        for (String w : getNextWords(current, wordList, next)) {
            if (w.equals(current) 
                    || !dist.containsKey(w)
                    || dist.get(current) - dist.get(w) != 1) {
                continue;
            }
            now.add(w);
            help(res, now, dist, next, wordList, target);
            now.remove(now.size() - 1);
        }
    }
    
    public List<List<String>> findLadders(String beginWord, String endWord, Set<String> wordList) {
        HashMap<String, Integer> dist = new HashMap<String, Integer>();
        HashMap<String, List<String>> next = new HashMap<String, List<String>>();
        LinkedList<String> q = new LinkedList<String>();
        q.offer(beginWord);
        dist.put(beginWord, 1);
        
        // bfs
        int len = 1;
        while (!q.isEmpty()) {
            int size = q.size();
            for (int i = 0; i < size; i++) {
                String s = q.poll();
                if (s.equals(endWord)) {
                    break;
                }
                for (String w : getNextWords(s, wordList, next)) {
                    if (dist.containsKey(w)) {
                        continue;
                    }
                    dist.put(w, len + 1);
                    q.offer(w);
                }
            }
            len++;
        }
        // dfs
        List<List<String>> res = new ArrayList<List<String>>();
        List<String> now = new ArrayList<String>();
        now.add(endWord);
        help(res, now, dist, next, wordList, beginWord);
        return res;
    }
}
```
