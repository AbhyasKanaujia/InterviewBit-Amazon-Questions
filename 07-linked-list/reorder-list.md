# ⭐ Reorder List

{% embed url="https://www.interviewbit.com/problems/reorder-list/" %}

<details>

<summary>Inefficient Solution: 1st attempt</summary>

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
 
ListNode *getSecondToLast(ListNode *ll) {
    while(ll -> next -> next) 
        ll = ll -> next;
        
    return ll;
}
 
ListNode* Solution::reorderList(ListNode* A) {
    ListNode* first = A;
    while(first -> next && first -> next -> next) {
        ListNode* prev = getSecondToLast(first);
        ListNode* last = prev -> next;
        last -> next = first -> next;
        first -> next = last;
        prev -> next = NULL;
        first = last -> next;
    }
    
    return A;
}
```

</details>

### Efficient: Breaking the list in two halves

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
 
ListNode *reverseLinkedList(ListNode *A) {
    ListNode *prev = NULL, *current = A;
    
    while(current) {
        ListNode *next = current -> next;
        current -> next = prev;
        prev = current;
        current = next;
    }
    
    return prev;
}
ListNode* Solution::reorderList(ListNode* A) {
    if(!A || !A -> next) return A;
    
    ListNode *slow = A, *fast = A;
    while(fast && fast -> next && fast -> next -> next) {
        slow = slow -> next;
        fast = fast -> next -> next;
    }
    ListNode *secondHalf = slow -> next;
    slow -> next = NULL;
    ListNode *firstHalf = A;
    
    secondHalf = reverseLinkedList(secondHalf);
    
    while(secondHalf) {
        ListNode *next1 = firstHalf -> next;
        ListNode *next2 = secondHalf -> next;
        
        firstHalf -> next = secondHalf;
        secondHalf -> next = next1;
        
        firstHalf = next1;
        secondHalf = next2;
    }
    return A;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(1)$$​
