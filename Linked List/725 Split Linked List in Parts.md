**Problem**

Given a (singly) linked list with head node  `root`, write a function to split the linked list into  `k`  consecutive linked list "parts".

The length of each part should be as equal as possible: no two parts should have a size differing by more than 1. This may lead to some parts being null.

The parts should be in order of occurrence in the input list, and parts occurring earlier should always have a size greater than or equal parts occurring later.

Return a List of ListNode's representing the linked list parts that are formed.

Examples 1->2->3->4, k = 5 // 5 equal parts [ [1], [2], [3], [4], null ]

**Example 1:**  

**Input:** 
root = [1, 2, 3], k = 5
**Output:** [[1],[2],[3],[],[]]

**Example 2:**  

**Input:** 
root = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10], k = 3
**Output:** [[1, 2, 3, 4], [5, 6, 7], [8, 9, 10]]

**Solution**
```
class Solution {
public:
    vector<ListNode*> splitListToParts(ListNode* root, int k) {
        int N = 0;
        ListNode* cur = root;
        while(cur != NULL){
            N++;
            cur = cur -> next;
        }
        
        int width = N / k, rem = N % k;
        cur = root;
        vector<ListNode*> ans;
        for(int i = 0; i < k; i++){
            ans.push_back(cur);
            for(int j = 0; j < width + (i < rem? 1 : 0) - 1; j++)
                if(cur != NULL)
                    cur = cur -> next;
            if(cur != NULL){
                ListNode* pre = cur;
                cur = cur -> next;
                pre -> next = NULL;
            }
        }
        return ans;        
    }
};
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTczNTA5NTA3XX0=
-->