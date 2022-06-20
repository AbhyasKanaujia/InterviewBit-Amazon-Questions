# Intersection of Linked Lists

{% embed url="https://www.interviewbit.com/problems/intersection-of-linked-lists/" %}

### Using set to track visited nodes

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
ListNode* Solution::getIntersectionNode(ListNode* A, ListNode* B) {
    set<ListNode*> s;
    ListNode *ptr = A;
    while(ptr) {
        s.insert(ptr);
        ptr = ptr -> next;
    }
    
    ptr = B;
    while(ptr) {
        if(s.count(ptr))
            return ptr;
        s.insert(ptr);
        ptr = ptr -> next;
    }
    
    return NULL;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(n)$$​

### Ignoring Nodes from Longer Linked List

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
 
int getLen(ListNode *p) {
    int count = 0;
    
    while(p) {
        count++;
        p = p -> next;
    }
    
    return count;
}

ListNode *getNode(ListNode *A, int n) {        
    while(--n) 
        A = A -> next;
    
    return A;
}

ListNode* Solution::getIntersectionNode(ListNode* A, ListNode* B) {
    int n1 = getLen(A);
    int n2 = getLen(B);
    
    if(!n1 || !n2)
        return NULL;
    
    // make sure A is shorter than B
    if(n1 > n2) 
        return getIntersectionNode(B, A);
        
    
    ListNode *ptr1 = A;
    ListNode *ptr2;
    if(n2 > n1)
        ptr2 = getNode(B, n2 - n1) -> next;
    else   
        ptr2 = B;
    
    while(ptr1 && ptr2) 
        if(ptr1 == ptr2) 
            return ptr1;
        else {
            ptr1 = ptr1 -> next;
            ptr2 = ptr2 -> next;
        }        
        
    return NULL;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(1)$$​
