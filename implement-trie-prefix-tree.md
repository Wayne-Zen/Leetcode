[Link](https://leetcode.com/problems/implement-trie-prefix-tree/)


```java
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

    // Returns if the word is in the trie.
    public boolean search(String word) {
        TrieNode node = root;
        for (char c : word.toCharArray()) {
            if (!node.map.containsKey(c)) {
                return false;
            } 
            node = node.map.get(c);
        }
        return node.end;
    }

    // Returns if there is any word in the trie
    // that starts with the given prefix.
    public boolean startsWith(String prefix) {
        TrieNode node = root;
        for (char c : prefix.toCharArray()) {
            if (!node.map.containsKey(c)) {
                return false;
            } 
            node = node.map.get(c);
        }
        return true;
    }
}

// Your Trie object will be instantiated and called as such:
// Trie trie = new Trie();
// trie.insert("somestring");
// trie.search("key");
```
