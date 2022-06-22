# ⭐ Kth Node From Middle

{% embed url="http://www.interviewbit.com/problems/kth-node-from-middle/" %}

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
 
int getLength(ListNode *ll) {
    int count = 0;
    while(ll) {
        count++;
        ll = ll->next;
    }
    
    return count;
}

int Solution::solve(ListNode* A, int B) {
    int length = getLength(A);
    
    int mid = length / 2 + 1;
    int k = mid - B;
    
    ListNode *ptr = A;
    
    if(k <= 0)
        return -1;
            
    for(int i = 1; i < k; i++) 
        ptr = ptr->next;
    
    return ptr -> val;    
}

```
