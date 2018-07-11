**Problem**

Given a linked list, return the node where the cycle begins. If there is no cycle, return  `null`.

**Note:**  Do not modify the linked list.

**Solution**
```
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode *slow = head, *fast = head;
        bool nocycle = true;
        if(!head || !head -> next)
            return NULL;
        while(fast -> next && fast -> next -> next){
            slow = slow -> next;
            fast = fast ->next -> next;
            if(slow == fast){
                nocycle = false;
                break;
            }
        }
        if(nocycle == true)
            return NULL;
        fast = head;
        while(fast != slow){
            fast = fast -> next;
            slow = slow -> next;
        }
        return slow;
    }
};
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTMyMjIyNTA0XX0=
-->