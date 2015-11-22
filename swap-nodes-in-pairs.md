[Link](https://leetcode.com/problems/swap-nodes-in-pairs/)

<img src="https://lh3.googleusercontent.com/8mvE3OSHkRGNdc84AI9H-mvBPVZWX0bkzW2nMhM_SSJbpJc0Ng3_Lqr1nlzlhZWeNOcKNx9G99igGRA-4AJm-FWEUljIelmqrRU7kf6dMVbgNR6q3BEPlsQDJ1R90mDQH8ajFel5PVaiE03_BNBc-MclQsUOgozu1CZqCJtzRiCYSJcANukRngDJfv_0GMEM8V4B9q2dUjsGMF4iwqL2DHv49n5L-huV3Ik56hW5vxbLEHOsAOqD8lPVI9-ucuX7EvA4P2TLwuQN1y4I8wgu27hQbXYBKrGYpLSGcVY2WJkEWYRUFsnOnH5gSNbo0BmB0G-q97F-NWaFFDuYchlXaVAuuNave23A6nLrQj1gIPQM-5miM-KlkR4twKaMe2-mkwfbOXxhF2-NAf15BKn5x3NARESXEJ28-qsfiSwH5gNkDIVLCct_G5l4ZBQYUcLZbrjw2Xdt_JSNrurLjOddTXzSc6Nb5hWMRW2MKsXV9wqSR8lsvVZau4mi87EyXPNh7IwGFc_a3STyUtotcFp2bjShqA7mGD8_PCRrvN1zuaI=w1728-h893-no" width="300">

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
    public ListNode swapPairs(ListNode head) {
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode n1, n2, n3, n4;
        n1 = dummy;
        while (true) {
            if (n1 == null) {
                break;
            }
            n2 = n1.next;
            if (n2 == null) {
                break;
            }
            n3 = n1.next.next;
            if (n3 == null) {
                break;
            }
            n4 = n1.next.next.next;
            n1.next = n3;
            n3.next = n2;
            n2.next = n4;
            // 坑： 已经交换过了
            n1 = n2;
        }
        return dummy.next;
    }
}
```
