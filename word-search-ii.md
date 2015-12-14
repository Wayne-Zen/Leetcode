[Link](https://leetcode.com/problems/word-search-ii/)

```java
public class Solution {
    public List<String> findWords(char[][] board, String[] words) {
        List<String> res = new ArrayList<String>();
        boolean[][] visited = new boolean[board.length][board[0].length];
        TrieTree tree = new TrieTree();
        for (String word : words) {
            tree.insert(word);
        }
        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                if (!tree.prefix("" + board[i][j])) {
                    continue;
                }
                visited[i][j] = true;
                help(res, "" +  board[i][j], board, i, j, visited, tree);
                visited[i][j] = false;
            }
        }
        return res;
    }
    
    private void help(List<String> res, String now, char[][] board,
                      int row, int col, boolean[][] visited, TrieTree tree) {
        if (tree.search(now) && !res.contains(now)) {
            res.add(now);
        }
        int[] rAdd = {1, -1, 0, 0};
        int[] cAdd = {0, 0, 1, -1};
        for (int i = 0; i < 4; i++) {
            int r = row + rAdd[i];
            int c = col + cAdd[i];
            if (r < 0 || r >= board.length || c < 0 || c >= board[0].length
                    || visited[r][c] || !tree.prefix(now + board[r][c])) {
                continue;
            }
            visited[r][c] = true;
            help(res, now + board[r][c], board, r, c, visited, tree);
            visited[r][c] = false;
        }
    }
    
    class TreeNode {
        boolean isEnd = false;
        HashMap<Character, TreeNode> map = new HashMap<Character, TreeNode>();
    }
    
    class TrieTree {
        TreeNode root = new TreeNode();
        public void insert(String s) {
            TreeNode node = root;
            for (char c : s.toCharArray()) {
                if (node.map.containsKey(c)) {
                    node = node.map.get(c);
                } else {
                    node.map.put(c, new TreeNode());
                    node = node.map.get(c);
                }
            }
            node.isEnd = true;
        }
        public boolean search(String s) {
            TreeNode node = root;
            for (char c : s.toCharArray()) {
                if (node.map.containsKey(c)) {
                    node = node.map.get(c);
                } else {
                    return false;
                }
            }
            return node.isEnd;
        }
        public boolean prefix(String s) {
            TreeNode node = root;
            for (char c : s.toCharArray()) {
                if (node.map.containsKey(c)) {
                    node = node.map.get(c);
                } else {
                    return false;
                }
            }
            return true;
        }
    }
}
```
