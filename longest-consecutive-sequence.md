[Link](https://leetcode.com/problems/longest-consecutive-sequence/)

```java
public class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        HashSet<Integer> set = new HashSet<Integer>();
        for (int n : nums) {
            set.add(n);
        }
        int max = 0;
        for (int n : nums) {
            if (!set.contains(n)) {
                continue;
            }
            int len = 1;
            int n1 = n - 1;
            int n2 = n + 1;
            while (set.contains(n1)) {
                if (set.contains(n1)) {
                    len++;
                    set.remove(n1);
                    n1--;
                }
            }
            while (set.contains(n2)) {
                if (set.contains(n2)) {
                    len++;
                    set.remove(n2);
                    n2++;
                }
            }
            max = Math.max(max, len);
        }
        return max;
    }
}
```
```java
public class Solution {
    class UF {
        int[] rank;
        int[] parent;
        int[] cnt;
        public UF(int n) {
            rank = new int[n];
            parent = new int[n];
            cnt = new int[n];
            for (int i = 0; i < n; i++) {
                rank[i] = 1;
                parent[i] = i;
                cnt[i] = 1;
            }
        }
        public int find(int x) {
            while (x != parent[x]) {
                parent[x] = parent[parent[x]];
                x = parent[x];
            }
            return x;
        }
        public void union(int x, int y) {
            int rootX = find(x);
            int rootY = find(y);
            if (rootX == rootY) {
                return;
            }
            int cntX = cnt[rootX];
            int cntY = cnt[rootY];
            int sum = cntX + cntY;
            cnt[rootX] = sum;
            cnt[rootY] = sum;
            
            if (rank[rootX] < rank[rootY]) {
                parent[rootX] = rootY;
            } else if (rank[rootX] > rank[rootY]) {
                parent[rootY] = rootX;
            } else if (rank[rootX] == rank[rootY]){
                parent[rootY] = rootX;
                rank[rootX]++;
            }
        }
        public int maxCnt() {
            int res = 0;
            for (int i = 0; i < cnt.length; i++) {
                res = Math.max(res, cnt[i]);
            }
            return res;
        }
    }
    public int longestConsecutive(int[] nums) {
        // val -> index
        HashMap<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length; i++) {
            map.put(nums[i], i);
        }
        UF uf = new UF(nums.length);
        for (int i = 0; i < nums.length; i++) {
            int val = nums[i];
            if (map.containsKey(val + 1)) {
                uf.union(map.get(val), map.get(val + 1));
            }
            if (map.containsKey(val - 1)) {
                uf.union(map.get(val), map.get(val - 1));
            }
        }
        return uf.maxCnt();
    }
}
```
