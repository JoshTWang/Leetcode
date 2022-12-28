#### Top Down Merge Sort

```java
class Solution {
    public ListNode sortList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode mid = getMid(head);
        ListNode left = sortList(head);
        ListNode right = sortList(mid);
        return merge(left, right);
    }
    
    // 21.MergeTwoSortedLists
    public ListNode merge(ListNode left, ListNode right) {
        if (left == null) {
            return right;
        }
        if (right == null) {
            return left;
        }
        if (left.val < right.val) {
            left.next = merge(left.next, right);
            return left;
        } else {
            right.next = merge(left, right.next); 
            return right;
        }
    }
    // tortoise and hare
    public ListNode getMid(ListNode head) {
        ListNode slowPrev = new ListNode(61, head);
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slowPrev = slowPrev.next;
        }
        ListNode slow = slowPrev.next;
        slowPrev.next = null;
        return slow;
    }
}
```

