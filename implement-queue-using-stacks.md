[Link](https://leetcode.com/problems/implement-queue-using-stacks/)

```java
import java.util.*;

class MyQueue {
    Stack<Integer> s1 = new Stack<Integer>();
    Stack<Integer> s2 = new Stack<Integer>();
    // Push element x to the back of queue.
    public void push(int x) {
        s1.push(x);
    }

    // Removes the element from in front of queue.
    public void pop() {
        if (!empty()) {
            s2.pop();
        } else {
            throw new EmptyStackException();
        }
    }

    // Get the front element.
    public int peek() {
        if (!empty()) {
            return s2.peek();
        } else {
            throw new EmptyStackException();
        }
    }

    // Return whether the queue is empty.
    public boolean empty() {
        if (!s2.isEmpty()) {
            return false;
        } else {
            while (!s1.isEmpty()) {
                s2.push(s1.pop());
            }
            return s2.isEmpty();
        }
    }
}
```
