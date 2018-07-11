**Problem**
Reverse a singly linked list.
**Example:**
**Input:** 1->2->3->4->5->NULL
**Output:** 5->4->3->2->1->NULL

**Solution**
Using iteration:
```
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* prev = NULL;
        while(head != NULL){
            ListNode * nextnode = head -> next;
            head -> next = prev;
            prev = head;
            head = nextnode;
        }
        return prev;
    }
};
```
Using recursion
```
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(head == NULL || head -> next == NULL)
            return head;
        ListNode* p = reverseList(head -> next);
        head -> next -> next = head;
        head -> next = NULL;
        return p;
    }
};
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDk1MjYxMDM5LC0yODEyMTgzNDJdfQ==
-->