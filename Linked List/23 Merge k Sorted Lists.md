**Problem**

Merge  _k_  sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

**Example:**

**Input:**
[
  1->4->5,
  1->3->4,
  2->6
]
**Output:** 1->1->2->3->4->4->5->6

**Solution**

Using heap
```
class Solution {
public:
    class mycomp{
    public:
        bool operator() (ListNode* a, ListNode* b) const{
            return a -> val > b -> val;
        }
    };
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        if(lists.size() == 0)
            return NULL;
        priority_queue<ListNode*, vector<ListNode*>, mycomp> q;
        for(auto i : lists){
            if(i != NULL)
                q.push(i);
        }
        ListNode* head = new ListNode(0), *cur = head;
        while(!q.empty()){
            ListNode* x = q.top();
            q.pop();
            cur -> next = x;
            cur = cur -> next;
            if(x -> next)
                q.push(x -> next);
        }
        return head -> next;
    }
};
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI3ODIyOTQ3NF19
-->