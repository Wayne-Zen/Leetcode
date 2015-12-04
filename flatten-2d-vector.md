[Link](https://leetcode.com/problems/flatten-2d-vector/)

```java
public class Vector2D {
    Iterator<List<Integer>> lItr;
    Iterator<Integer> iItr;

    public Vector2D(List<List<Integer>> vec2d) {
        lItr = vec2d.iterator();
        iItr = lItr.hasNext() ? lItr.next().iterator() : null;
    }

    public int next() {
        hasNext();
        return iItr.next();
    }

    public boolean hasNext() {
        if(iItr==null)
            return false;
        else if(iItr.hasNext())
            return true;
        else {
            while(lItr.hasNext()) {
                iItr = lItr.next().iterator();
                if(iItr.hasNext())
                    return true;
            }
            return false;
        }
    }
}
```
