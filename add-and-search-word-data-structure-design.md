[Link](https://leetcode.com/problems/add-and-search-word-data-structure-design/)

```java
public class WordDictionary {
    class TreeNode {
        boolean isEnd = false;
        HashMap<Character, TreeNode> map = new HashMap<Character, TreeNode>();
    }
    
    TreeNode root = new TreeNode();
    // Adds a word into the data structure.
    public void addWord(String word) {
        TreeNode node = root;
        for (char c : word.toCharArray()) {
            if (!node.map.containsKey(c)) {
                node.map.put(c, new TreeNode());
            }
            node = node.map.get(c);
        }
        node.isEnd = true;
    }

    // Returns if the word is in the data structure. A word could
    // contain the dot character '.' to represent any one letter.
    public boolean search(String word) {
        return searchHelp(word, 0, root);
    }
    private boolean searchHelp(String s, int pos, TreeNode node) {
        if (pos == s.length()) {
            return node.isEnd;
        }
        char c = s.charAt(pos);
        if (c == '.') {
            for (char x : node.map.keySet()) {
                if (searchHelp(s, pos + 1, node.map.get(x))) {
                    return true;
                }
            }
            return false;
        } else if (node.map.containsKey(c)) {
            return searchHelp(s, pos + 1, node.map.get(c));
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
