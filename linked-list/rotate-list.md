# Rotate List

12 min

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
        ll = ll -> next;
    }
    return count;
}

ListNode* getEnd(ListNode *ll) {
    if(!ll) return ll;
    
    while(ll -> next)
        ll = ll -> next;
        
    return ll;
}

ListNode* Solution::rotateRight(ListNode* A, int B) {
    int n = getLength(A);
    B = B % n;
    int end = n - B;
    
    if(end == 0 || B == 0)
        return A;
    
    int count = 1;    
    ListNode *ptr = A;
    
    while(count < end) {
        count++;
        ptr = ptr -> next;
    }
    
    ListNode *start = ptr -> next;
    ptr -> next = NULL;
    
    getEnd(start) -> next = A;
    return start;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(1)$$​
