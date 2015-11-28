[Link](https://leetcode.com/problems/add-and-search-word-data-structure-design/)

```java
public class WordDictionary {
    private class TrieNode {
        boolean isEnd = false;
        HashMap<Character, TrieNode> map = new HashMap<Character, TrieNode>();
    }
    
    TrieNode root = new TrieNode();

    // Adds a word into the data structure.
    public void addWord(String word) {
        TrieNode node = root;
        for (char c : word.toCharArray()) {
            if (!node.map.containsKey(c)) {
                node.map.put(c, new TrieNode());
            }
            node = node.map.get(c);
        }
        node.isEnd = true;
    }

    // Returns if the word is in the data structure. A word could
    // contain the dot character '.' to represent any one letter.
    public boolean search(String word) {
        return mySearch(word, 0, root);
    }
    
    public boolean mySearch(String word, int index, TrieNode node) {
        if (index == word.length()) {
            return node.isEnd;
        }
        char c = word.charAt(index);
        if (node.map.containsKey(c)) {
            return mySearch(word, index + 1, node.map.get(c));
        } else if (c == '.') {
            for (TrieNode n : node.map.values()) {
                if (mySearch(word, index + 1, n)) {
                    return true;
                }
            }
            return false;
        } else {
            return false;
        }
    }
}

// Your WordDictionary object will be instantiated and called as such:
// WordDictionary wordDictionary = new WordDictionary();
// wordDictionary.addWord("word");
// wordDictionary.search("pattern");
```
