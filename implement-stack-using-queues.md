[Link](https://leetcode.com/problems/implement-stack-using-queues/)

```java
class MyStack {
    Queue<Integer> q1 = new LinkedList<Integer>();
    Queue<Integer> q2 = new LinkedList<Integer>();
    
    // Push element x onto stack.
    public void push(int x) {
        q1.offer(x);
        while (!q2.isEmpty()) {
            q1.offer(q2.poll());
        }
        Queue<Integer> temp = q2;
        q2 = q1;
        q1 = temp;
    }

    // Removes the element on top of the stack.
    public void pop() {
        q2.poll();
    }

    // Get the top element.
    public int top() {
        return q2.peek();
    }

    // Return whether the stack is empty.
    public boolean empty() {
        return q2.isEmpty();
    }
}
```
