
* 三个主要私有方法：
  1. removeFirst
  2. removeNode
  3. addToTail
* 分开`removeNode`和`addToTail`
* `removeFirst`依赖于`removeNode`的实现
* dummynode: head, tail
* 同时管理 map 和 双向链表

<img src="https://lh3.googleusercontent.com/y2JryHgdkZmDFDB4wpEY3ovPutbY06DCiJAWQI_X57bhwYTh0QykHCEdULNqn9wVKSQVLH3WRQQdUytVVuNjzgL82iTA0i-cVGrhGZqHYtK6JAjXqEU1re6n2_QRMB7GUso5ivLlsWKbh6kF3kn9WXIx-O7EB_gBPFWf78RDZF3VU91oS1J345EbgXJo0JQi_LFkyq82NzMo16N6u2mzdXNAKaCIaz5PkSHmCkTl3h_RWnLhaBjIyMoAbDdH1ovF4Tcv6CL43SWl5mC-fFCLfCIMcM2jnnGRFuathutxS5wXMvDOZy7t9YjVzPdvp5AKgSl7ZHHNGmVp55DdgZf11HL2FMJouZU7OemOGoxaoS_DCvNJ_IX3C0fY4p-elitdLs8o1jW2dnBCVtjPqON_cWCeQtzVBvUbcIqvApoDnGPHJUPcyk6fZZjDBboR1sAbnbiYSHtTJgzxpdDWWN-SlnEgH2gp9Xie7UQAusX34UmvI_1LpXZ8qRhZX5fMcX2vmdS-PsbcPoOPV6V1dbT98dwSAhHS9R6Ywm1oz3dlr-U=w1728-h1122-no" width="200">
```java
public class LRUCache {
    private class Dlink {
        Dlink prev;
        Dlink next;
        int key;
        int val;
        Dlink(int key, int val) {
            this.key = key;
            this.val = val;
            prev = null;
            next = null;
        }
    }
    
    int capacity;
    HashMap<Integer, Dlink> map;
    Dlink head;
    Dlink tail;
    
    private void removeFirst() {
        removeNode(head.next);
    }
    
    private void removeNode(Dlink node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }
    
    private void addToTail(Dlink node) {
        tail.prev.next = node;
        
        node.prev = tail.prev;
        node.next = tail;
        
        tail.prev = node;
    }
    
    
    public LRUCache(int capacity) {
        this.capacity = capacity;
        map = new HashMap<Integer, Dlink>();
        head = new Dlink(-1, -1);
        tail = new Dlink(-1, -1);
        head.next = tail;
        tail.prev = head;
    }
    
    public int get(int key) {
        Dlink node = map.get(key);
        if (node == null) {
            return -1;
        }
        
        removeNode(node);
        addToTail(node);
        
        return node.val;
    }
    
    public void set(int key, int value) {
        Dlink node = map.get(key);
        if (node == null) {
            node = new Dlink(key, value);
            map.put(key, node);
        } else {
            node.val = value;
            removeNode(node);
        }
        
        addToTail(node);
        
        if (map.size() > capacity) {
            map.remove(head.next.key);
            removeFirst();
        }
    }
}
```
