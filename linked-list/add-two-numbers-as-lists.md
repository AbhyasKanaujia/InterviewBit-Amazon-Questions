# Add Two Numbers as Lists

{% embed url="https://www.interviewbit.com/problems/add-two-numbers-as-lists/" %}

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
ListNode* Solution::addTwoNumbers(ListNode* A, ListNode* B) {
    ListNode *res = new ListNode(0);
    ListNode *ptr = res;
    
    int carry = 0;
    
    while(A || B || carry) {
        int sum = 0;
        
        if(A) {
            sum += A -> val;
            A = A -> next;
        }
        
        if(B) {
            sum += B -> val;
            B = B -> next;
        }   
        
        sum += carry;
        
        ptr -> next = new ListNode(sum % 10);
        ptr = ptr -> next;
        
        carry = sum / 10;
    }
    
    
    return res -> next;
}

```
