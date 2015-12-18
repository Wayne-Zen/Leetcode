[Link](https://leetcode.com/problems/implement-queue-using-stacks/)

```java
import java.util.EmptyStackException;

class MyQueue {
    
    Stack<Integer> s1 = new Stack<Integer>();
    Stack<Integer> s2 = new Stack<Integer>();
    
    // Push element x to the back of queue.
    public void push(int x) {
        s1.push(x);
    }

    // Removes the element from in front of queue.
    public void pop() {
        if (empty()) {
            throw new EmptyStackException();
        }
        s2.pop();
    }

    // Get the front element.
    public int peek() {
        if (empty()) {
            throw new EmptyStackException();
        }
        return s2.peek();
    }

    // Return whether the queue is empty.
    public boolean empty() {
        if (s2.isEmpty()) {
            if (s1.isEmpty()) {
                return true;
            }
            while (!s1.isEmpty()) {
                s2.push(s1.pop());
            }
        }
        return false;
    }
}
```
