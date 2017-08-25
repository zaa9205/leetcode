# leetcode

**You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.**

**You may assume the two numbers do not contain any leading zero, except the number 0 itself.**

**Input: (2 -> 4 -> 3) + (5 -> 6 -> 4);
Output: 7 -> 0 -> 8**

Solution - need to consider below cases, (9) + (1), the result should be (0,1) because the carry is 1.

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode s1 = l1;
        ListNode s2 = l2;
        ListNode anslist = new ListNode(0);
        ListNode current = anslist;
        int sum = 0;
        
        while (s1 != null || s2 != null || sum / 10 != 0) {
            sum /= 10;
            if (s1 != null) {
                sum += s1.val;
                s1 = s1.next;
            }
            if (s2 != null) {
                sum += s2.val;
                s2 = s2.next;
            }            
            current.next = new ListNode(sum % 10);
            current = current.next;
        }      
        //final carry is 1;
        //if(sum / 10 != 0) {  
        //    current.next = new ListNode(sum / 10);
        //}
        
        return anslist.next;
    }
}
```
