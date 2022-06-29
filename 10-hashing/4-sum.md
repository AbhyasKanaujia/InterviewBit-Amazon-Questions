# ⭐ 4 Sum



## Brute Force: 4 Pointers

{% tabs %}
{% tab title="C++" %}
```cpp
vector<vector<int> > Solution::fourSum(vector<int> &A, int B) {
    sort(A.begin(), A.end());
    set<vector<int>> s;
    for(int i = 0; i < A.size(); i++)
        for(int j = i + 1; j < A.size(); j++)
            for(int k = j + 1; k < A.size(); k++)
                for(int l = k + 1; l < A.size(); l++) 
                    if(A[i] + A[j] + A[k] + A[l] == B){
                        vector<int> quard = {A[i], A[j], A[k], A[l]};
                        s.insert(quard);
                    }
               
    vector<vector<int>> res(s.begin(), s.end());            
    return res;
}
```

Accepted
{% endtab %}
{% endtabs %}

Time Complexity: $$O(n^5\log n)$$

Space Complexity: $$O(n)$$

## Using Two pointer technique

{% embed url="https://www.youtube.com/watch?v=4ggF3tXIAp0" %}

{% tabs %}
{% tab title="C++" %}
```cpp
vector<vector<int> > Solution::fourSum(vector<int> &A, int B) {
    vector<vector<int>> res;
    
    if(A.empty())
        return res;
        
    int n = A.size();
    // sort to use two poitners
    sort(A.begin(), A.end());
    
    for(int i = 0; i < n; i++) {
        for(int j = i + 1; j < n; j++) {
            int target = B - A[i] - A[j];
            int front = j + 1;
            int back = n - 1;
            while(front < back) {
                int twoSum = A[front] + A[back];
                if(twoSum < target) front++;
                else if(twoSum > target) back--;
                else {
                    vector<int> quard = {A[i], A[j], A[front], A[back]};
                    res.push_back(quard);
                    
                    while(front < back && A[front] == quard[2]) front++;
                    while(front < back && A[back] == quard[3]) back--;
                }
            }
            
            while(j + 1 < n && A[j + 1] == A[j]) j++;
        }
        
        while(i + 1 < n && A[i + 1] == A[i]) i++;
    }
        
    return res;
}
```
{% endtab %}
{% endtabs %}
