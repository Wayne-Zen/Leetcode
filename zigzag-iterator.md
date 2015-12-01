[Link](https://leetcode.com/problems/zigzag-iterator/)

```java
public class ZigzagIterator {

    boolean b1 = true;
    Iterator<Integer> it1;
    Iterator<Integer> it2;
    public ZigzagIterator(List<Integer> v1, List<Integer> v2) {
        this.it1 = v1.iterator();
        this.it2 = v2.iterator();
    }

    public int next() {
        if (it1.hasNext() && it2.hasNext()) {
            if (b1) {
                b1 = !b1;
                return it1.next();
            } else {
                b1 = !b1;
                return it2.next();
            }
        }
        if (it1.hasNext()) {
            return it1.next();
        } else { // (it2.hasNext())
            return it2.next();
        }
    }

    public boolean hasNext() {
        return it1.hasNext() || it2.hasNext();
    }
}

/**
 * Your ZigzagIterator object will be instantiated and called as such:
 * ZigzagIterator i = new ZigzagIterator(v1, v2);
 * while (i.hasNext()) v[f()] = i.next();
 */
```
