[Link](https://leetcode.com/problems/peeking-iterator/)

```java
// Java Iterator interface reference:
// https://docs.oracle.com/javase/8/docs/api/java/util/Iterator.html
class PeekingIterator implements Iterator<Integer> {
    private Iterator<Integer> iterator;
    private Integer save;
    private boolean saved = false;
    
	public PeekingIterator(Iterator<Integer> iterator) {
	    // initialize any member here.
	    this.iterator = iterator;
	}

    // Returns the next element in the iteration without advancing the iterator.
	public Integer peek() {
	    if (saved) {
            return save;
	    } else {
	        save = next();
            saved = true;
            return save;
	    }
	}

	// hasNext() and next() should behave the same as in the Iterator interface.
	// Override them if needed.
	@Override
	public Integer next() {
	    if (saved) {
	        saved = false;
	        return save;
	    } else {
	        return iterator.next();
	    }
	}

	@Override
	public boolean hasNext() {
	    if (saved) {
	        return true;
	    } else {
	        return iterator.hasNext();
	    }
	}
}
```
