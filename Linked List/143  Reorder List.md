**Problem**

Given a singly linked list  _L_:  _L_0→_L_1→…→_L__n_-1→_L_n,  
reorder it to:  _L_0→_L__n_→_L_1→_L__n_-1→_L_2→_L__n_-2→…

You may  **not**  modify the values in the list's nodes, only nodes itself may be changed.

**Example 1:**

Given 1->2->3->4, reorder it to 1->4->2->3.

**Example 2:**

Given 1->2->3->4->5, reorder it to 1->5->2->4->3.

**Solution**

1.Find the middle of the list
2.Reverse the half after middle  1->2->3->4->5->6 to 1->2->3->6->5->4
3,Start reorder one by one  1->2->3->6->5->4 to 1->6->2->5->3->4

```c
lass Solution {
public:
    void reorderList(ListNode* head) {
        if(head == NULL || head -> next == NULL)
            return;
        
        ListNode *slow = head, *fast = head;
        while(fast ->next && fast -> next -> next){
            slow = slow -> next;
            fast = fast -> next -> next;
        }
        
        ListNode *pre = NULL, *cur = slow -> next;
        while(cur){
            ListNode* nextnode = cur -> next;
            cur -> next = pre;
            pre = cur;
            cur = nextnode;
        }
        
        ListNode *FirstMid = head, *SecondMid = pre;
        while(FirstMid != slow){
            ListNode *firstnext = FirstMid -> next;
            ListNode *secondnext = SecondMid -> next;
            FirstMid -> next = SecondMid;
            SecondMid -> next = firstnext;
            FirstMid = firstnext;
            SecondMid = secondnext;
        }
        FirstMid -> next = SecondMid;
    }
};
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4MjUwMTYyMDUsOTQ1MTIxMTgxXX0=
-->