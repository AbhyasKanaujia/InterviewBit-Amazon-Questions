# ⭐ K reverse linked list

{% embed url="https://www.interviewbit.com/problems/k-reverse-linked-list/" %}

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
 
ListNode* reverse(ListNode *ll) {
    ListNode *prev = NULL;
    ListNode *current = ll;
    
    while(current) {
        ListNode *next = current -> next;
        
        current -> next = prev;
        
        prev = current;
        current = next;
    }
            
    return prev;
}

ListNode* Solution::reverseList(ListNode* A, int k) {
    ListNode *dummy = new ListNode(-1);
    dummy -> next = A;
    
    ListNode *beforeCurrentSegment = dummy;
    ListNode *segmentLast = dummy;
    while(segmentLast -> next) {
        ListNode *segmentFirst = beforeCurrentSegment -> next;
        
        for(int i = 1; i <= k && segmentLast->next; i++)
            segmentLast = segmentLast->next;
            
        ListNode *afterSegment = segmentLast->next;
        
        segmentLast->next = NULL;
        
        reverse(segmentFirst);
        beforeCurrentSegment->next = segmentLast;
        segmentFirst->next = afterSaegment;
        
        beforeCurrentSegment = segmentLast = segmentFirst;        
    }
    
    return dummy->next;
}

```
