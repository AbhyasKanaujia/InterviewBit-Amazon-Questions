# ⭐ Find Duplicate in Array

{% embed url="https://www.interviewbit.com/problems/find-duplicate-in-array/" %}

## Techniques

| Technique   | Time Complexity | Sapce Complexity      |
| ----------- | --------------- | --------------------- |
| Brute Force | $$O(n^2)$$      | $$O(1)$$              |
| Sorting     | $$O(n\log n)$$​ | $$O(n)$$ or $$O(1)$$​ |
| Set/Map     | $$O(n)$$​       | $$O(n)$$              |

## Brute Force

{% tabs %}
{% tab title="CPP" %}
```cpp
int Solution::repeatedNumber(const vector<int> &A) {
    for(int i = 0; i < A.size(); i++)
        for(int j = i + 1; j < A.size(); j++)
            if(A[i] == A[j])
                return A[i];
                
    return -1;
}
```

<mark style="color:red;">Time Limit Exceed</mark>
{% endtab %}

{% tab title="JS" %}
```javascript
module.exports = { 
 //param A : array of integers
 //return an integer
    repeatedNumber : function(A){
        for(let i = 0; i < A.length; i++)
            for(let j = i + 1; j < A.length; j++)
                if(A[i] == A[j])
                    return A[i];
                    
        return -1;
    }
};
```

<mark style="color:red;">Time Limit Exceed</mark>
{% endtab %}
{% endtabs %}

Time Complexity: $$O(n^2)$$​

Space Complexity: $$O(1)$$​

## Using Sorting

{% tabs %}
{% tab title="CPP" %}
```cpp
int Solution::repeatedNumber(const vector<int> &A) {
    vector<int> copy(A.begin(), A.end());
    sort(copy.begin(), copy.end());
    int prev = copy[0];
    for(int i = 1; i < copy.size(); i++) 
        if(copy[i] == prev)    
            return copy[i];
        else
            prev = copy[i];
            
    return prev;
}
```

<mark style="color:green;">Accepted</mark>
{% endtab %}

{% tab title="JS" %}
```javascript
module.exports = { 
  //param A : array of integers
  //return an integer
  repeatedNumber : function(A){
    A.sort()
    
    prev = A[0]
    for(let i = 1; i < A.length; i++)
      if(A[i] == prev)
        return A[i]
      else
        prev = A[i]
  }
};
```

<mark style="color:green;">Accepted</mark>
{% endtab %}
{% endtabs %}

Time Complexity: $$O(n \log n)$$​

Space Complexity: $$O(n)$$​ for duplicating `const` array.

## Using Set

{% tabs %}
{% tab title="CPP" %}
```cpp
int Solution::repeatedNumber(const vector<int> &A) {
    set<int> s;
    for(const int &x: A)
        if(s.count(x))
            return x;
        else
            s.insert(x);
            
    return -1;
}
```

<mark style="color:red;">Memory Limit Exceed</mark>
{% endtab %}

{% tab title="JS" %}
```javascript
module.exports = { 
    //param A : array of integersa
    //return an integer
    repeatedNumber : function(A){
        let s = new Set()
        
        for(let x of A)
            if(s.has(x))
                return x
            else
                s.add(x)
    }
};
```

<mark style="color:green;">Accepted</mark>
{% endtab %}
{% endtabs %}

Time Complexity: $$O(n)$$​

Space Complexity: $$O(n)$$​

## Tortoise Hare

{% embed url="https://www.youtube.com/watch?v=32Ll35mhWg0" %}

```cpp
int Solution::repeatedNumber(const vector<int> &A) {
    int slow = A[0];
    int fast = A[0];
    
    do {
        slow = A[slow];
        fast = A[A[fast]];
    } while(slow != fast);
    
    slow = A[0];
    
    while(slow != fast) {
        slow = A[slow];
        fast = A[fast];
    }
    
    return slow;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(1)$$​
