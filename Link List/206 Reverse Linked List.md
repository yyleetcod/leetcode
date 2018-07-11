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
eyJoaXN0b3J5IjpbLTI4MTIxODM0Ml19
-->