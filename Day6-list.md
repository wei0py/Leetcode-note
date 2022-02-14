### Day6 Linked List
## Leetcode 206. Reverse Linked List
```python
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if not head:
            return head
        reverse = ListNode(None)
        temp = None
        while head:
            reverse = head
            head = reverse.next
            reverse.next = temp
            temp = reverse
        return reverse
```
## Leetcode 876. Middle of the Linked List



## Leetcode 160. Intersection of Two Linked Lists
## Leetcode 141. Linked List Cycle (Linked List Cycle II)
## Leetcode 92. Reverse Linked List II





## Leetcode 328. Odd Even Linked List
