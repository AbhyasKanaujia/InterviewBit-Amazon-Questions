---
cover: >-
  https://images.unsplash.com/photo-1534126416832-a88fdf2911c2?crop=entropy&cs=tinysrgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHw4fHxkaXZpZGV8ZW58MHx8fHwxNjU5NzE0ODYx&ixlib=rb-1.2.1&q=80
coverY: 727.361963190184
---

# ⭐ Square Root of Integer



{% embed url="https://www.interviewbit.com/search/?q=Amazon" %}

{% tabs %}
{% tab title="C++" %}
```cpp
int Solution::sqrt(int A) {
    if(A == 0) return 0;

    int low = 1, high = A, res;

    while(low <= high) {
        int mid = low + ((high - low) >> 1);
        if(mid <= A / mid) {
            low = mid + 1;
            res = mid;
        } else 
            high = mid - 1;
    }
    return res;
}
```
{% endtab %}

{% tab title="JS" %}
````javascript
sqrt : function(A){
    if(A == 0)  return A;
    let low = 1, high = A;
    
    while(low <= high) {
        mid = low + ((high - low) >> 1);
        
        if(mid * mid < A) {
            low = mid + 1;
            res = mid;
        } else if (mid * mid > A)
            high = mid - 1;
        else
            return mid;
    }
    
    return res;
}```

````
{% endtab %}
{% endtabs %}

Time Complexity: $$O(\log n)$$​

Space Complexity: $$O(1)$$​

Edge case: $$A = 0$$​
