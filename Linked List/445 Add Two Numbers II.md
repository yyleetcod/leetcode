**Problem**
You are given two  **non-empty**  linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Follow up:**  
What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

**Example:**

**Input:** (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
**Output:** 7 -> 8 -> 0 -> 7

**Solution**
```
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int len1 = GetLength(l1), len2 = GetLength(l2);
        ListNode* head = new ListNode(0);
        if(len1 >= len2)
            head -> next = helper(l1, l2, len1 - len2);
        else
            head -> next = helper(l2, l1, len2 - len1);
        if(head -> next -> val > 9){
            head -> val++;
            head -> next -> val -= 10;
            return head;
        }
        else
            return head -> next;
    }
    int GetLength(ListNode* l){
        int len = 0;
        while(l){
            len++;
            l = l -> next;
        }
        return len;
    }
    ListNode* helper(ListNode* l1, ListNode* l2, int len){
        if(l1 == NULL)
            return NULL;
        ListNode* ans = len != 0? new ListNode(l1 -> val) : new ListNode(l1 -> val + l2 -> val);
        ListNode* post = len == 0? helper(l1 -> next, l2 -> next, 0) : helper(l1 -> next, l2, len - 1);
        if(post != NULL && post -> val > 9){
            ans -> val = ans -> val + 1;
            post -> val = post -> val - 10;
        }
        ans -> next = post;
        return ans;
    }
};
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA0Mzg4NTUyNl19
-->