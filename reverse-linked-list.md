[Link](https://leetcode.com/problems/reverse-linked-list/)

<img src="https://lh3.googleusercontent.com/PJaUE7-UX-8nt-M8nRHnQSe92CulwrpAxkfibrVNQQHC88_u1xbwQUMq9ofEgCY71nUOQkj4h80y5-h8RhCP3v2sE5AMjUEtG9d8TwZslXKYsM5e0txqNn45pjXnPofI4ntm9YOKxe_by4tagZ3uWh-H1JjWESYt3jhFUraM2vWWpFUO1gIZbE7zcs5iYqCUy25Y6IBM-zaj7lf89hry3DaPbfGLSqsNmxgxF1yY3lB8sAezYRQ9szv9xeqEBUBHuJIy3fxTzWkGKykBU9zreu9Hz7XXo678fvKNMRFXzbGuxmlmF7Q_KI7oi138FdvCslss913niMfBJHqc-vNzx9ZNIl2uiVMejkw8RMuFTtKhQuJvnmqf4PPvNjsS4eUzUDU0aE9GZm-kyUt2IJCJGuFbaHHkejtiVgRjOJsSdUoRMoYYl6GU0RN6VIn6KUeVBQuGO9_KQVBMUvyT0P89_0cQmFPXZLSeKA-6mS_zJ9vgWWX4BtEjpFMeSVSFcDJ27TN9OYtETkaWfHCrG6jP876oTwzOzGpgIABJQiwZuAs=w1728-h1296-no" width="300">

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
    public ListNode reverseList(ListNode head) {
        if(head == null || head.next == null) {
            return head;
        }
     
        ListNode p1 = head;
        ListNode p2 = head.next;
        
        // init key point
        head.next = null;
        
        while(p1 != null && p2 != null){
            ListNode tmp = p2.next;
            p2.next = p1;
            p1 = p2;
            if (tmp!=null){
                p2 = tmp;
            }else{
                break;
            }
        }
        return p2;
    }
}
```
