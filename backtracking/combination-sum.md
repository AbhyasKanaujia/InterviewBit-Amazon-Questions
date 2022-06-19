# ⭐ Combination Sum

{% embed url="https://www.interviewbit.com/problems/combination-sum/hints/" %}

```cpp
set<vector<int>> res;

void getWays(vector<int> &A, int B, int current, vector<int> &output) {
    if(B == 0) {
        res.insert(output);
        return;
    }
    
    for(int i = current; i < A.size(); i++) {
        if(B - A[i] >= 0) {
            output.push_back(A[i]);
            getWays(A, B - A[i], i, output);
            output.pop_back();
        }
    }
}

vector<vector<int> > Solution::combinationSum(vector<int> &A, int B) {
    res.clear();
    sort(A.begin(), A.end());
    int current = 0;
    vector<int> output;
    getWays(A, B, current, output);
    vector<vector<int>> ways(res.begin(), res.end());
    return ways;    
}
```

<mark style="color:red;">Edge Case: If the input has duplicate</mark> values, <mark style="color:red;">then the result will also have duplicate values. This needs to emit.</mark>&#x20;

<mark style="color:green;">Handling: Either make the given input unique and sorted. Or use the set as used in the above code.</mark>&#x20;
