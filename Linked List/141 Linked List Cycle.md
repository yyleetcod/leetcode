**Problem**

Given a linked list, determine if it has a cycle in it.

**Solution**

1.Hash Table
-   Time complexity :  $O(n)$. We visit each of the  nn  elements in the list at most once. Adding a node to the hash table costs only  $O(1)$ time.
    
-   Space complexity:  $O(n)$. The space depends on the number of elements added to the hash table, which contains at most  $n$  elements.

2.Slow/fast pointer
```
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if(!head || !head -> next)
            return false;
        ListNode * slow = head;
        ListNode * fast = head;
        while(fast -> next && fast ->next ->next){
            slow = slow -> next;
            fast = fast -> next -> next;
            if(slow == fast)
                return true;
        }
        return false;
    }
};
```
Analyse:
-   Time complexity :  $O(n)$. Let us denote  $n$  as the total number of nodes in the linked list. To analyze its time complexity, we consider the following two cases separately.
    
    -   **_List has no cycle:_**  
        The fast pointer reaches the end first and the run time depends on the list's length, which is $O(n)$.
        
    -   **_List has a cycle:_**  
        We break down the movement of the slow pointer into two steps, the non-cyclic part and the cyclic part:
        
        1.  The slow pointer takes "non-cyclic length" steps to enter the cycle. At this point, the fast pointer has already reached the cycle.  $\text{Number of iterations} = \text{non-cyclic length} = N$
            
        2.  Both pointers are now in the cycle. Consider two runners running in a cycle - the fast runner moves 2 steps while the slow runner moves 1 steps at a time. As the distance is at most $"\text{cyclic length K}"$ and the speed difference is 1, we conclude that  
            $\text{Number of iterations} = \text{almost "cycle length K"}$.
              
    Therefore, the worst case time complexity is  $O(N+K)$, which is  $O(n)$.
    
-   Space complexity :  $O(1)$. We only use two nodes (slow and fast) so the space complexity is  $O(1)$.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyNzI0NDk0OThdfQ==
-->