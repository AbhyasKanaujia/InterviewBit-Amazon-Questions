# Copy List

<mark style="color:red;">Can be done without a</mark> <mark style="color:orange;">map,</mark> <mark style="color:red;">using interleaving and detaching!</mark>

## Using Map

{% tabs %}
{% tab title="C++" %}
```cpp
/**
 * Definition for singly-linked list.
 * struct RandomListNode {
 *     int label;
 *     RandomListNode *next, *random;
 *     RandomListNode(int x) : label(x), next(NULL), random(NULL) {}
 * };
 */
RandomListNode* Solution::copyRandomList(RandomListNode* A) { 
    map<RandomListNode *, RandomListNode *> oldToNewMap;
    map<RandomListNode *, RandomListNode *> nodeToRandomMap;
    
    
    for(RandomListNode *ptr = A; ptr; ptr = ptr->next) {
        RandomListNode *newNode = new RandomListNode(ptr->label);
        oldToNewMap[ptr] = newNode;
        nodeToRandomMap[ptr] = ptr->random;
    }
    
    for(RandomListNode *ptr = A; ptr; ptr = ptr->next) {
        oldToNewMap[ptr]->next = oldToNewMap[ptr->next];
        oldToNewMap[ptr]->random = oldToNewMap[ptr->random];
    }
    
    return oldToNewMap[A];
}
```

Accepted
{% endtab %}
{% endtabs %}

Time Complexity: $$O(n)$$​

Space Complexity: $$O(2n)$$​
