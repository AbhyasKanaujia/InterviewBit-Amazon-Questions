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
