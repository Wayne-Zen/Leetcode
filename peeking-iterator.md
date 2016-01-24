[Link](https://leetcode.com/problems/peeking-iterator/)

```java
// Java Iterator interface reference:
// https://docs.oracle.com/javase/8/docs/api/java/util/Iterator.html
class PeekingIterator implements Iterator<Integer> {
    boolean peeked = false;
    Integer peekedVal = 0;
    Iterator<Integer> iter;
	public PeekingIterator(Iterator<Integer> iterator) {
	    // initialize any member here.
	    iter = iterator;
	}

    // Returns the next element in the iteration without advancing the iterator.
	public Integer peek() {
	    if (peeked) {
	        return peekedVal;
	    } else {
            peeked = true;
            peekedVal = iter.next();
            return peekedVal;
	    }
	}

	// hasNext() and next() should behave the same as in the Iterator interface.
	// Override them if needed.
	@Override
	public Integer next() {
	    if (peeked) {
	        peeked = false;
	        return peekedVal;
	    } else {
	        return iter.next();
	    }
	}

	@Override
	public boolean hasNext() {
	    if (peeked) {
	        return true;
	    } else {
	        return iter.hasNext();
	    }
	}
}
```
