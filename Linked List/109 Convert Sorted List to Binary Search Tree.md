**Problem**

Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of  _every_  node never differ by more than 1.

**Example:**

Given the sorted linked list: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:
```
      0
     / \
   -3   9
   /   /
 -10  5
 ```
**Soluton**
```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
    ListNode* list;
public:
    TreeNode* sortedListToBST(ListNode* head) {
        int size = 0;
        ListNode* cur = head;
        while(cur){
            size++;
            cur = cur -> next;
        }
        list = head;
        TreeNode* node = GenerateBST(size);
        return node;
    }
    TreeNode* GenerateBST(int n){
        if(n == 0)
            return NULL;
        TreeNode* parent = new TreeNode(0);
        parent -> left = GenerateBST(n / 2);
        parent -> val = list -> val;
        list = list -> next;
        parent -> right = GenerateBST(n - n / 2 - 1);
        return parent;
    }
};
```
Analyze:
Divide and Conquer, but we should first generate its left child tree, then the parent node, finally we generate the right child tree， rather than parent node -> left child tree -> right child tree($O(nlogn)$). Only in this way can we access the node of the Listnode in sequence.
- Time Complexity: $O(n)$
- Space Complexity: $O(1)$
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4MDExNjEzMV19
-->