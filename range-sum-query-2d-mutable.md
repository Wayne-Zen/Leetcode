[Link](https://leetcode.com/problems/range-sum-query-2d-mutable/)

* 与1D的不同在于，四个子节点，可以有的为空，有的不为空

```java
public class NumMatrix {
    class TreeNode {
        int r1;
        int c1;
        int r2;
        int c2;
        int sum;
        TreeNode lu;
        TreeNode ru;
        TreeNode ld;
        TreeNode rd;
    }
    
    class SegmentTree {
        TreeNode root = new TreeNode();
        public void build(int[][] matrix) {
            root = buildHelp(matrix, 0, 0, matrix.length - 1, matrix[0].length - 1);
        }
        public TreeNode buildHelp(int[][] matrix, int r1, int c1, int r2, int c2) {
            if (r1 > r2 || c1 > c2) {
                return null;
            }
            TreeNode node = new TreeNode();
            node.r1 = r1;
            node.r2 = r2;
            node.c1 = c1;
            node.c2 = c2;
            if (r1 == r2 && c1 == c2) {
                node.sum = matrix[r1][c1];
                return node;
            } else {
                int rmid = r1 + (r2 - r1) / 2;
                int cmid = c1 + (c2 - c1) / 2;
                node.lu = buildHelp(matrix, r1, c1, rmid, cmid);
                node.ru = buildHelp(matrix, r1, cmid + 1, rmid, c2);
                node.ld = buildHelp(matrix, rmid + 1, c1, r2, cmid);
                node.rd = buildHelp(matrix, rmid + 1, cmid + 1, r2, c2);
                node.sum = (node.lu == null ? 0 : node.lu.sum)
                         + (node.ru == null ? 0 : node.ru.sum)
                         + (node.ld == null ? 0 : node.ld.sum)
                         + (node.rd == null ? 0 : node.rd.sum);
                return node;
            }
        }
        public void modify(int r, int c, int val) {
            modifyHelp(root, r, c, val);
        }
        public void modifyHelp(TreeNode node, int r, int c, int val) {
            if (node == null) {
                return;
            }
            if (r == node.r1 && r == node.r2 && c == node.c1 && c == node.c2) {
                node.sum = val;
                return;
            } 
            if (r < node.r1 || r > node.r2 || c < node.c1 || c > node.c2) {
                return;
            }
            int rmid = node.r1 + (node.r2 - node.r1) / 2;
            int cmid = node.c1 + (node.c2 - node.c1) / 2;
            modifyHelp(node.lu, r, c, val);
            modifyHelp(node.ru, r, c, val);
            modifyHelp(node.ld, r, c, val);
            modifyHelp(node.rd, r, c, val);
            node.sum = (node.lu == null ? 0 : node.lu.sum)
                     + (node.ru == null ? 0 : node.ru.sum)
                     + (node.ld == null ? 0 : node.ld.sum)
                     + (node.rd == null ? 0 : node.rd.sum);
        }
        public int query(int r1, int c1, int r2, int c2) {
            return queryHelp(root, r1, c1, r2, c2);
        }
        public int queryHelp(TreeNode node, int r1, int c1, int r2, int c2) {
            if (node == null) {
                return 0;
            }
            // total overlap
            if (r1 <= node.r1 && c1 <= node.c1 && r2 >= node.r2 && c2 >= node.c2) {
                return node.sum;
            }
            // no overlap
            if (node.r2 < r1 || node.c2 < c1 || r2 < node.r1 || c2 < node.c1) {
                return 0;
            }
            // partial overlap
            return queryHelp(node.lu, r1, c1, r2, c2)
                 + queryHelp(node.ru, r1, c1, r2, c2)
                 + queryHelp(node.ld, r1, c1, r2, c2)
                 + queryHelp(node.rd, r1, c1, r2, c2);
        }
    }
    
    SegmentTree tree = new SegmentTree();
    
    public NumMatrix(int[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return;
        }
        tree.build(matrix);
    }

    public void update(int row, int col, int val) {
        tree.modify(row, col, val);
    }

    public int sumRegion(int row1, int col1, int row2, int col2) {
        return tree.query(row1, col1, row2, col2);
    }
}


// Your NumMatrix object will be instantiated and called as such:
// NumMatrix numMatrix = new NumMatrix(matrix);
// numMatrix.sumRegion(0, 1, 2, 3);
// numMatrix.update(1, 1, 10);
// numMatrix.sumRegion(1, 2, 3, 4);
```

