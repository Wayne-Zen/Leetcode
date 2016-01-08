[Link](https://leetcode.com/problems/zigzag-iterator/)

```java
public class ZigzagIterator {
    Iterator<Integer> iter1;
    Iterator<Integer> iter2;
    boolean p1 = true;
    public ZigzagIterator(List<Integer> v1, List<Integer> v2) {
        if (v1 != null) {
            iter1 = v1.iterator();
        }
        if (v2 != null) {
            iter2 = v2.iterator();
        }
    }

    public int next() {
        if (iter1 != null && iter1.hasNext() && iter2 != null && iter2.hasNext()) {
            int res = 0;
            if (p1) {
                res = iter1.next();
            } else {
                res = iter2.next();
            }
            p1 = !p1;
            return res;
        } else if (iter1 != null && iter1.hasNext()) {
            return iter1.next();
        } else if (iter2 != null && iter2.hasNext()){
            return iter2.next();
        } else {
            return 0;
        }
    }

    public boolean hasNext() {
        return (iter1 != null && iter1.hasNext()) || (iter2 != null && iter2.hasNext());
    }
}

/**
 * Your ZigzagIterator object will be instantiated and called as such:
 * ZigzagIterator i = new ZigzagIterator(v1, v2);
 * while (i.hasNext()) v[f()] = i.next();
 */
```
