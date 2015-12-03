[Link](https://leetcode.com/problems/find-the-celebrity/)

```java
/* The knows API is defined in the parent class Relation.
      boolean knows(int a, int b); */

public class Solution extends Relation {
    public int findCelebrity(int n) {
        List<Integer> candi = new ArrayList<Integer>();
        for (int i = 0; i < n; i++) {
            candi.add(i);
        }
        while (candi.size() > 1) {
            List<Integer> newCan = new ArrayList<Integer>();
            for (int i = 1; i < candi.size(); i += 2) {
                if (knows(candi.get(i - 1), candi.get(i))) {
                    newCan.add(candi.get(i));
                } else {
                    newCan.add(candi.get(i - 1));
                }
            }
            if (candi.size() % 2 == 1) {
                newCan.add(candi.get(candi.size() - 1));
            }
            candi = newCan;
        }
        
        int res = candi.get(0);
        for (int i = 0; i < n; i++) {
            if (i != res) {
                if (knows(res, i) || !knows(i, res)) {
                    return -1;
                }
            }
        }
        return res;
    }
}
```
