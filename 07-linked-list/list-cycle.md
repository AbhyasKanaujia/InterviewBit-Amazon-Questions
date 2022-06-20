# ⭐ List Cycle

{% embed url="https://www.interviewbit.com/problems/list-cycle/" %}

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
ListNode* Solution::detectCycle(ListNode* A) {
    // Do not write main() function.
    // Do not read input, instead use the arguments to the function.
    // Do not print the output, instead return values as specified
    // Still have a doubt. Checkout www.interviewbit.com/pages/sample_codes/ for more details
    ListNode *slow = A, *fast = A;
    while(fast && fast -> next && fast -> next -> next) {
        slow = slow -> next;
        fast = fast -> next -> next;
        if(slow == fast) break;
    }
    
    if(slow != fast) 
        return NULL;
        
    slow = A;
    while(slow != fast) {
        slow = slow -> next;
        fast = fast -> next;
    }
    
    return slow;
}

```
