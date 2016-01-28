
[Link](https://leetcode.com/problems/lru-cache/)

<img src="img/Photos/lru-cache.png" width="400">
```java
public class LRUCache {
    class ListNode {
        int key;
        int value;
        ListNode prev;
        ListNode next;
        public ListNode(int key, int value) {
            this.key = key;
            this.value = value;
        }
    }
    // key -> node
    HashMap<Integer, ListNode> map = new HashMap<Integer, ListNode>();
    int capacity;
    ListNode head;
    ListNode tail;
    
    private void remove(ListNode node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }
    
    private void append(ListNode node) {
        ListNode prevNode = tail.prev;
        prevNode.next = node;
        node.next = tail;
        tail.prev = node;
        node.prev = prevNode;
    }
    
    public LRUCache(int capacity) {
        this.capacity = capacity;
        head = new ListNode(-1, -1);
        tail = new ListNode(-1, -1);
        head.next = tail;
        tail.prev = head;
    }
    
    public int get(int key) {
        if (map.containsKey(key)) {
            ListNode node = map.get(key);
            remove(node);
            append(node);
            return node.value;
        } else {
            return -1;
        }
    }
    
    public void set(int key, int value) {
        if (map.containsKey(key)) {
            ListNode node = map.get(key);
            remove(node);
            node.value = value;
            append(node);
        } else {
            ListNode node = new ListNode(key, value);
            map.put(key, node);
            append(node);
        }
        if (map.size() > capacity) {
            ListNode del = head.next;
            remove(del);
            map.remove(del.key);
        }
    }
}
```
