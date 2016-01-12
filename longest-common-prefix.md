[Link](https://leetcode.com/problems/longest-common-prefix/)

* 外层循环string， 内层循环char
* first string as target
* 检查不同string长度导致的下标越界, e.g.["hi", "hello"]

```java
public class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length == 0) {
            return "";
        }
        ArrayList<Character> res = new ArrayList<Character>();
        for (int i = 0; i < strs[0].length(); i++) {
            boolean allPass = true;
            char c = strs[0].charAt(i);
            for (int j = 1; j < strs.length; j++) {
                if (i >= strs[j].length() || strs[j].charAt(i) != c) {
                    allPass = false;
                    break;
                }
            }
            if (allPass) {
                res.add(c);
            } else {
                break;
            }
        }
        StringBuilder sb = new StringBuilder();
        for (char c : res) {
            sb.append(c);
        }
        return sb.toString();
    }
}
```

```java
public class Solution {
    class TrieNode {
        // Initialize your data structure here.
        HashMap<Character, TrieNode> map = new HashMap<Character, TrieNode>();
        boolean end = false;
        public TrieNode() {
        }
    }
    
    public class Trie {
        private TrieNode root;
    
        public Trie() {
            root = new TrieNode();
        }
    
        // Inserts a word into the trie.
        public void insert(String word) {
            TrieNode node = root;
            for (char c : word.toCharArray()) {
                if (!node.map.containsKey(c)) {
                    node.map.put(c, new TrieNode());
                } 
                node = node.map.get(c);
            }
            node.end = true;
        }
    
        public String getLongestPrefix() {
            TrieNode node = root;
            StringBuilder sb = new StringBuilder();
            while (!node.end && node.map.size() == 1) {
                for (char c : node.map.keySet()) {
                    sb.append(c);
                    node = node.map.get(c);
                }
            }
            return sb.toString();
        }
    }
    
    public String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length == 0) {
            return "";
        }
        Trie tree = new Trie();
        for (String str : strs) {
            tree.insert(str);
        }
        return tree.getLongestPrefix();
    }
}
```
