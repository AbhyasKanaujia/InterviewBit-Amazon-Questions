# ⭐ Reverse Alternate K Nodes

{% embed url="https://www.interviewbit.com/problems/reverse-alternate-k-nodes/" %}

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
    ListNode *previous = NULL;
    ListNode *current = ll;
    
    while(current) {
        ListNode *next = current->next;
        
        current -> next = previous;
        
        previous = current;
        current = next;
    }
    return previous;
}

ListNode* Solution::solve(ListNode* A, int B) {
    bool skip = false;
    
    // used as negative space
    ListNode *dummy = new ListNode(-1);
    dummy -> next = A;
    
    ListNode *beforeSegment = dummy;
    ListNode *segmentLast = dummy;
    
    while(segmentLast->next) {
        ListNode *segmentFirst = beforeSegment -> next;
        
        for(int i = 1; i <= B && segmentLast -> next; i++)
            segmentLast = segmentLast->next;
        
        if(!skip) {
            ListNode *afterSegment = segmentLast->next;    
            segmentLast -> next = NULL;
            reverse(segmentFirst);
            beforeSegment -> next = segmentLast;
            segmentFirst -> next = afterSegment;
            beforeSegment = segmentLast = segmentFirst;
        } else {
            beforeSegment = segmentLast;
        }
        skip = !skip;
    }
    
    return dummy->next;
}
```
