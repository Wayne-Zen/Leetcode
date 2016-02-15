[Link](https://leetcode.com/problems/flatten-2d-vector/)

```java
public class Vector2D {

    Iterator<List<Integer>> lIter;
    Iterator<Integer> iIter;

    public Vector2D(List<List<Integer>> vec2d) {
        lIter = vec2d.iterator();
    }

    public int next() {
        return iIter.next();
    }

    public boolean hasNext() {
        while ((iIter == null || !iIter.hasNext()) && lIter.hasNext()) {
            iIter = lIter.next().iterator();
        }
        // iIter != null && iIter.hasNext()
        return !(iIter == null || !iIter.hasNext());
    }
}

/**
 * Your Vector2D object will be instantiated and called as such:
 * Vector2D i = new Vector2D(vec2d);
 * while (i.hasNext()) v[f()] = i.next();
 */
```
