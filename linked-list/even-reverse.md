# ⭐ Even Reverse

{% embed url="https://www.interviewbit.com/problems/even-reverse/" %}

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
 
ListNode *reverse(ListNode *ll) {
    ListNode *prev = NULL;
    ListNode *current = ll;
    
    while(current) {
        ListNode *next = current->next;
        
        current->next = prev;
        
        prev = current;
        current = next;
    }
    
    return prev;
}

ListNode* Solution::solve(ListNode* A) {
    ListNode *odd = new ListNode(-1);
    ListNode *even = new ListNode(-1);
    ListNode *res = new ListNode(-1);
    
    ListNode *oddPtr = odd;
    ListNode *evenPtr = even;
    ListNode *listPtr = A;
    ListNode *resPtr = res;
    
    // separete even and odd values 
    bool evenPos = false;
    while(listPtr) {
        if(evenPos) {
            evenPtr -> next = listPtr;
            evenPtr = evenPtr -> next;
        } else {
            oddPtr -> next = listPtr;
            oddPtr = oddPtr -> next;
        }
        
        evenPos = !evenPos;
        listPtr = listPtr -> next;
    }
    
    oddPtr->next = NULL;
    evenPtr->next = NULL;
    
    // reverse even values
    even->next = reverse(even->next);
    
    oddPtr = odd->next;
    evenPtr = even->next;
    
    // interweave
    while(oddPtr && evenPtr) {
        resPtr->next = oddPtr;
        oddPtr = oddPtr->next;
        resPtr = resPtr->next;
        
        resPtr->next = evenPtr;
        evenPtr = evenPtr->next;
        resPtr = resPtr->next;        
    }
    
    while(oddPtr) {        
        resPtr->next = oddPtr;
        oddPtr = oddPtr->next;
        resPtr = resPtr->next;
    }
    
    while(evenPtr) {
        resPtr->next = evenPtr;
        evenPtr = evenPtr->next;
        resPtr = resPtr->next; 
    }
    
    resPtr->next = NULL;
    
    return res->next;
    
}
```
