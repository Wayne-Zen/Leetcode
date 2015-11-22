[Link](https://leetcode.com/problems/merge-k-sorted-lists/)

* 注意PriorityQueue的使用
  * 构造函数第一个参数是size， 不能为0，所以输入参数检查必要
  * 重写Comparator

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    private class MyComparator implements Comparator<ListNode> {
        public int compare(ListNode n1, ListNode n2) {
            return n1.val - n2.val;
        }
    }
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) {
            return null;
        }
        PriorityQueue<ListNode> queue = new PriorityQueue<ListNode>(lists.length, new MyComparator());
        for (int i = 0; i < lists.length; i++) {
            if (lists[i] != null) {
                queue.offer(lists[i]);
            }
        }
        ListNode dummy = new ListNode(-1);
        ListNode now = dummy;
        while (!queue.isEmpty()) {
            ListNode node = queue.poll();
            now.next = node;
            now = now.next;
            if (node.next != null) {
                queue.offer(node.next);
            }
        }
        return dummy.next;
    }
}
```
