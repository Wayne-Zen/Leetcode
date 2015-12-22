[Link](https://leetcode.com/problems/copy-list-with-random-pointer/)

```java
/**
 * Definition for singly-linked list with a random pointer.
 * class RandomListNode {
 *     int label;
 *     RandomListNode next, random;
 *     RandomListNode(int x) { this.label = x; }
 * };
 */
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        if (head == null) {
            return null;
        }
        RandomListNode dummy = new RandomListNode(-1);
        dummy.next = head;
        while (head != null) {
            RandomListNode tmp = head.next;
            head.next = new RandomListNode(head.label);
            head.next.next = tmp;
            head = tmp;
        }
        head = dummy.next;
        while (head != null) {
            // 注意random指针为空
            if (head.random != null) {
                head.next.random = head.random.next;
            } else {
                head.next.random = null;
            }
            head = head.next.next;
        }
        head = dummy.next;
        RandomListNode cpDummy = new RandomListNode(-1);
        RandomListNode cp = cpDummy;
        while (head != null) {
            cp.next = head.next;
            head.next = head.next.next;  //还原初始链表
            head = head.next;
            cp = cp.next;
        }
        return cpDummy.next;
    }
}
```

```java
/**
 * Definition for singly-linked list with a random pointer.
 * class RandomListNode {
 *     int label;
 *     RandomListNode next, random;
 *     RandomListNode(int x) { this.label = x; }
 * };
 */
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        if (head == null) {
            return null;
        }
        RandomListNode save = head;
        HashMap<RandomListNode, RandomListNode> map = new HashMap<RandomListNode, RandomListNode>();
        while (head != null) {
            RandomListNode cp = new RandomListNode(head.label);
            map.put(head, cp);
            head = head.next;
        }
        for (RandomListNode s : map.keySet()) {
            RandomListNode r = map.get(s);
            r.next = map.get(s.next);
            r.random = map.get(s.random);
        }
        return map.get(save);
    }
}
```
