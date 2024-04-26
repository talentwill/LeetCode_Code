# 142. 环形链表 II

[[2024-04-26]]

```python
class Solution:
    def detectCycle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        slow = fast = head
        while slow and fast:
            slow = slow.next
            if not slow:
                return None # slow 没必要判断
            if not fast.next:
                return None
            fast = fast.next.next
            if slow == fast:
                while head != slow:
                    head = head.next
                    slow = slow.next
                return slow
        return None

```
