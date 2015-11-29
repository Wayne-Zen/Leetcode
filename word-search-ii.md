[Link](https://leetcode.com/problems/word-search-ii/)

```java
public class Solution {
    class TrieNode {
        boolean isEnd;
        HashMap<Character, TrieNode> map = new HashMap<Character, TrieNode>();
    }
    class TrieTree {
        TrieNode root = new TrieNode();
        public void insert(String word) {
            TrieNode node = root;
            for (char c : word.toCharArray()) {
                if (!node.map.containsKey(c)) {
                    node.map.put(c, new TrieNode());
                }
                node = node.map.get(c);
            }
            node.isEnd = true;
        }
        public boolean search(String word) {
            TrieNode node = root;
            for (char c : word.toCharArray()) {
                if (!node.map.containsKey(c)) {
                    return false;
                }
                node = node.map.get(c);
            }
            return node.isEnd;
        }
        public boolean prefix(String word) {
            TrieNode node = root;
            for (char c : word.toCharArray()) {
                if (!node.map.containsKey(c)) {
                    return false;
                }
                node = node.map.get(c);
            }
            return true;
        }
    }
    public List<String> findWords(char[][] board, String[] words) {
        List<String> res = new ArrayList<String>();
        StringBuilder now = new StringBuilder();
        if (board == null || board.length == 0 || board[0].length == 0
                || words == null || words.length == 0) {
            return res;
        }
        TrieTree trie = new TrieTree();
        for (String word : words) {
            trie.insert(word);
        }
        boolean[][] visited = new boolean[board.length][board[0].length];
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                now.append(board[i][j]);
                visited[i][j] = true;
                help(res, now, board, visited, trie, i, j);
                now.deleteCharAt(now.length() - 1);
                visited[i][j] = false;
            }
        }   
        return res;
    }
    private void help(List<String> res, StringBuilder now,
                      char[][] board, boolean[][] visited,
                      TrieTree trie, int row, int col) {
        if (!trie.prefix(now.toString())) {
            return;
        }
        if (trie.search(now.toString())) {
            if (!res.contains(now.toString())) {
                res.add(now.toString());
            }
            // 不能return，否则abc ab，永远找不到abc
            // 不同位置，可能搜到同一个结果
        }
        int[] rAdd = new int[]{0, 0, -1, 1};
        int[] cAdd = new int[]{-1, 1, 0, 0};
        for (int i = 0; i < 4; i++) {
            int r = row + rAdd[i];
            int c = col + cAdd[i];
            
            if (r < 0 || r >= board.length 
                    || c < 0 || c >= board[0].length
                    || visited[r][c]) {
                continue;       
            }
            now.append(board[r][c]);
            visited[r][c] = true;
            help(res, now, board, visited, trie, r, c);
            now.deleteCharAt(now.length() - 1);
            visited[r][c] = false;
        }
        
    }
}
```
