# Merge K Sorted Lists

{% embed url="https://www.interviewbit.com/problems/merge-k-sorted-lists/" %}

## 5 Approaches

| Approach                                | Time Complexity | Space Complexity |
| --------------------------------------- | --------------- | ---------------- |
| <p>Using Merge 2 Sorted </p><p>List</p> | $$O(nk)$$       | $$O(1)$$         |
| Using k pointers                        | $$O(nk)$$​      | O(1)             |
| Link All List and Merge Sort            | $$O(n\log n)$$  | $$O(1)$$         |
| Divide and Conquer                      | $$O(n\log k)$$​ | $$O(1)$$         |
|                                         |                 |                  |

{% embed url="https://youtu.be/kpCesr9VXDA" %}
Discusses 5 Approaches
{% endembed %}

## Using Merge 2 Sorted List

{% tabs %}
{% tab title="C++" %}
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
 
ListNode *merge2Lists(ListNode *A, ListNode *B) {
    ListNode *merged = new ListNode(-1);
    ListNode *mergedHead = merged;
    ListNode *ptr1 = A;
    ListNode *ptr2 = B;
    
    while(ptr1 && ptr2) {
        if(ptr1->val < ptr2->val) {
            merged->next = ptr1;
            ptr1 = ptr1->next;
        } else {
            merged->next = ptr2;
            ptr2 = ptr2->next;
        }
            
        merged = merged->next;
    }
    
    
    while(ptr1) {
        merged->next = ptr1;
        ptr1 = ptr1->next;
        merged = merged->next;
    }
    
    while(ptr2) {
        merged->next = ptr2;
        ptr2 = ptr2->next;
        merged = merged->next;
    }
    
    return mergedHead->next;    
}
ListNode* Solution::mergeKLists(vector<ListNode*> &A) {
    ListNode *merged = A[0];
    for(int i = 1; i < A.size(); i++) 
        merged = merge2Lists(merged, A[i]);
        
    return merged;
}
```

Accepted
{% endtab %}
{% endtabs %}

Time Complexity: $$O(kn)$$​ where $$n$$​ is the number of elements in each list.

Space Complexity: $$O(1)$$

## Compare All and Choose Min​

{% tabs %}
{% tab title="First Tab" %}
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
ListNode* Solution::mergeKLists(vector<ListNode*> &A) {
    ListNode *merged = new ListNode(-1);
    ListNode *mergedHead = merged;
    
    bool allNULL = false;
    while(true) {
        int i = 0;
        while(i < A.size() && !A[i]) 
            i++;
        
        if(i == A.size())
            break;
        
        int minNode = i;
        while(i < A.size()) {
            if(A[i] && A[i]->val < A[minNode]->val) {
                minNode = i;
                allNULL = false;
            }
            i++;
        }
        
        merged->next = A[minNode];
        
        A[minNode] = A[minNode]->next;
        merged = merged->next;
    }
    return mergedHead->next;
}
```

Accepted
{% endtab %}
{% endtabs %}

Time Complexity: $$O(nk)$$​

Space Complexity: $$O(1)$$

## Link all Linked List and Use Merge Sort

{% tabs %}
{% tab title="First Tab" %}
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
 
void link(ListNode *l1, ListNode *l2) {
    ListNode *ptr = l1;
    while(ptr -> next)
        ptr =  ptr -> next;
    
    ptr -> next = l2;
}

ListNode *getMid(ListNode *ll) {
    ListNode *slow = ll;
    ListNode *fast = ll;
    
    while(fast && fast->next && fast->next->next) {
        slow = slow->next;
        fast = fast->next->next;
    }
    
    return slow;
}

ListNode *merge(ListNode *l1, ListNode *l2) {
    if(!l1)
        return l2;
    
    if(!l2) 
        return l1;
        
    ListNode *head = (l1->val < l2->val) ? l1 : l2;
    while(l1 && l2)
        if(l1->val < l2->val) {
            ListNode* next = l1->next;
            if(!l1->next || l1->next->val >= l2->val) 
                l1->next = l2;            
            l1 = next;
        } else {
            ListNode *next = l2->next;
            if(!l2->next || l2->next->val > l1->val)
                l2->next = l1;
            l2 = next;
        }
    
    return head;
}

ListNode *mergeSort(ListNode *l1) {
    if(!l1 || !l1->next)
        return l1;
        
    ListNode *mid = getMid(l1);
    ListNode *l2 = mid->next;
    mid->next = NULL;
    l1 = mergeSort(l1);
    l2 = mergeSort(l2);
    return merge(l1, l2);
}

ListNode* Solution::mergeKLists(vector<ListNode*> &A) {
    ListNode *head = A[0];
    for(int i = 1; i < A.size(); i++)
        link(A[i - 1], A[i]); 
        
    return mergeSort(head);    
}
```

Accepted
{% endtab %}

{% tab title="Second Tab" %}

{% endtab %}
{% endtabs %}

Time Complexity: $$O(n \log k)$$​

Space Complexity: $$O(1)$$

### Notice Merge Function :star:​

{% tabs %}
{% tab title="C++" %}
```cpp
ListNode *merge(ListNode *l1, ListNode *l2) {
    if(!l1)
        return l2;
    
    if(!l2) 
        return l1;
        
    ListNode *head = (l1->val < l2->val) ? l1 : l2;
    while(l1 && l2)
        if(l1->val < l2->val) {
            ListNode* next = l1->next;
            if(!l1->next || l1->next->val >= l2->val)  // why >=? 
                l1->next = l2;            
            l1 = next;
        } else {
            ListNode *next = l2->next;
            if(!l2->next || l2->next->val > l1->val)
                l2->next = l1;
            l2 = next;
        }
    
    return head;
}

```
{% endtab %}
{% endtabs %}

## Dividing k Linked Lists into 2&#x20;

1. Divide the given $$K$$ Linked Lists into two parts until single LL remains
2. Backtrack and merge 2 Linked Lists at a time until is reached.&#x20;

{% tabs %}
{% tab title="C++" %}
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
 
ListNode *merge(ListNode *left, ListNode *right) {
    if(!left)   
        return right;
        
    if(!right)
        return left;
        
    ListNode *head = (left->val < right->val) ? left : right;
    while(left && right)
        if(left->val < right->val) {
            ListNode *next = left->next;
            if(!left->next || left->next->val >= right->val)
                left->next = right;
            
            left = next;
        } else {
            ListNode *next = right->next;
            if(!right->next || right->next->val > left->val)
                right->next = left;            
            right = next;
        }
    return head;
}
 
ListNode *DivideAndConquerMerge(vector<ListNode *> &A, int low, int high) {
    if(low >= high) 
        return A[low];
    
    int mid = low + ((high - low) >> 1);
    ListNode *left = DivideAndConquerMerge(A, low, mid);
    ListNode *right = DivideAndConquerMerge(A, mid + 1, high);
    
    return merge(left, right);    
}
ListNode* Solution::mergeKLists(vector<ListNode*> &A) {
    return DivideAndConquerMerge(A, 0, A.size() - 1);    
}
```

Accepted
{% endtab %}
{% endtabs %}

Time Complexity: $$O(n\log k)$$​

Space Complexity: $$O(1)$$​
