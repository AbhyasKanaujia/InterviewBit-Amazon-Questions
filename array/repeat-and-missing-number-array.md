# Repeat and Missing Number Array

{% embed url="https://www.interviewbit.com/problems/repeat-and-missing-number-array/" %}

| Approach           | Time Complexity | Space Complexity     | Remark                                     |
| ------------------ | --------------- | -------------------- | ------------------------------------------ |
| Negation Technique | $$O(n)$$        | $$O(1)$$ to $$O(n)$$ | Modification or duplication of given array |
| Using Sorting      | $$O(n\log n)$$​ | $$O(1)$$ to $$O(n)$$ | Modification or duplication of given array |
|                    |                 |                      |                                            |
|                    |                 |                      |                                            |
|                    |                 |                      |                                            |

## Negation Technique

{% tabs %}
{% tab title="C++" %}
```cpp
vector<int> Solution::repeatedNumber(const vector<int> &A) {
    vector<int> ACopy(A.begin(), A.end());
    vector<int> res;
    for(int i = 0; i < ACopy.size(); i++) 
        if(ACopy[abs(ACopy[i]) - 1] > 0)
            ACopy[abs(ACopy[i]) - 1] = -ACopy[abs(ACopy[i]) - 1];
        else 
            res.push_back(abs(ACopy[i]));
            
    
    for(int i = 0; i < ACopy.size(); i++)
        if(ACopy[i] > 0) {
            res.push_back(i + 1);
            break;
        }
        
    return res;
            
}
```

Accepted
{% endtab %}

{% tab title="JS" %}
```javascript
module.exports = { 
 //param A : array of integers
 //return a array of integers
	repeatedNumber : function(A){
        let res = []
        
        for(let i = 0; i < A.length; i++) 
            if(A[Math.abs(A[i]) - 1] > 0) 
                A[Math.abs(A[i]) - 1] = -A[Math.abs(A[i]) - 1]
            else 
                res.push(Math.abs(A[i]))
            
        for(let i = 0; i < A.length; i++)
            if(A[i] > 0) {
                res.push(i + 1)
                break
            }
            
        return res
	}
};
```

Accepted
{% endtab %}
{% endtabs %}

Time Complexity: $$O(n)$$

Space Complexity: $$O(n)$$ if `const` array. $$O(1)$$ with modification of given array.

## Using Sorting

{% tabs %}
{% tab title="C++" %}
```cpp
vector<int> Solution::repeatedNumber(const vector<int> &A) {
    int missing, repeated;
    
    vector<int> sorted(A.begin(), A.end());
    
    sort(sorted.begin(), sorted.end());
    
    if(sorted[0] != 1)
        missing = 1;
    if(sorted[sorted.size() - 1] !=  sorted.size())
        missing = sorted.size();
        
    for(int i = 1; i < sorted.size(); i++) {
        if(sorted[i] - sorted[i - 1] == 2)
            missing = sorted[i - 1] + 1;
            
        if(sorted[i] == sorted[i - 1])   
            repeated = sorted[i];
    }
    
    vector<int> res = {repeated, missing};
    return res;
}

```
{% endtab %}

{% tab title="JS" %}
```javascript
module.exports = { 
 //param A : array of integers
 //return a array of integers
	repeatedNumber : function(A){
        A.sort((a, b) => a - b)
        let missing = 0, repeated = 0;
        
        if(A[0] != 1)
            missing = 1;
        if(A[A.length - 1] != A.length)
            missing = A.length;
        for(let i = 1; i < A.length; i++) {
            if(A[i] - A[i - 1] == 2)
                missing = A[i - 1] + 1
            if(A[i] == A[i - 1])
                repeated = A[i]      
        }
        
        return[repeated, missing]
	}
};

```
{% endtab %}
{% endtabs %}

Time Complexity: $$O(n\log n)$$​

Space Complexity: $$O(n)$$​ if `const` array. $$O(1)$$​ with modification of the given array.&#x20;

## Using Arithmetic

```cpp
vector<int> Solution::repeatedNumber(const vector<int> &A) {
    long long n = A.size();
    
    long long sumN = n * (n + 1) / 2;
    long long sumN2 = n * (n + 1) * (2 * n + 1) / 6;
    
    long long sumA = 0;
    long long sumA2 = 0;

    for(const int &x: A) {
        sumA2 += x * x;
        sumA += x;
    }

    long long MissingMinusRepeating = sumN - sumA;
    long long Missing2MinusRepeating2 = sumN2 - sumA2;

    long long MissingPlusRepeating = Missing2MinusRepeating2 / MissingMinusRepeating;

    long long twiceMissing = MissingPlusRepeating + MissingMinusRepeating;
    long long twiceRepeating = MissingPlusRepeating - MissingMinusRepeating;

    vector<int> res = {twiceRepeating / 2, twiceMissing / 2};
    return res;
}
```
