**Problem**

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

**Solution**

```
/**
 * Definition for singly-linked list with a random pointer.
 * struct RandomListNode {
 *     int label;
 *     RandomListNode *next, *random;
 *     RandomListNode(int x) : label(x), next(NULL), random(NULL) {}
 * };
 */
class Solution {
public:
    unordered_map<RandomListNode *, RandomListNode *> mp;
    RandomListNode *copyRandomList(RandomListNode *head) {
        if(!head)
            return NULL;
        if(mp.count(head))
            return mp[head];
        
        RandomListNode *node = new RandomListNode(head -> label);
        mp[head] = node;
        node -> next = copyRandomList(head -> next);
        node -> random = copyRandomList(head -> random);
        
        return node;
    }
};
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU0OTk1MDEyMSwtNDE1NTMzMTQ0XX0=
-->