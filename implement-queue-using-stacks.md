[Link](https://leetcode.com/problems/implement-queue-using-stacks/)

```java
class MyQueue {
    Stack<Integer> stack1 = new Stack<Integer>();
    Stack<Integer> stack2 = new Stack<Integer>();
    
    // Push element x to the back of queue.
    public void push(int x) {
        stack1.push(x);
    }

    // Removes the element from in front of queue.
    public void pop() {
        empty();
        stack2.pop();
    }

    // Get the front element.
    public int peek() {
        empty();
        return stack2.peek();
    }

    // Return whether the queue is empty.
    public boolean empty() {
        if (!stack2.isEmpty()) {
            return false;
        } else {
            while (!stack1.isEmpty()) {
                stack2.push(stack1.pop());
            }
        }
        return stack2.isEmpty();
    }
}
```
