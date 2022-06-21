# 2 Sum

{% embed url="https://www.interviewbit.com/problems/2-sum/" %}

## Using Map

{% tabs %}
{% tab title="C++" %}
```cpp
vector<int> Solution::twoSum(const vector<int> &A, int B) {
    map<int, int> indexOf;
    vector<int> res;
    
    for(int i = 0; i < A.size(); i++)
        if(indexOf.count(B - A[i])) {
            res.push_back(indexOf[B - A[i]] + 1);
            res.push_back(i + 1);
            break;
        } else if (!indexOf.count(A[i]))
            indexOf[A[i]] = i;
            
    return res;
}
```

Accepted
{% endtab %}
{% endtabs %}

Time Complexity: $$O(n)$$​

Space Complexity: $$O(n)$$
