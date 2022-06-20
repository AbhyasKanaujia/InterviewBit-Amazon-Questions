# Combination Sum II

{% embed url="https://www.interviewbit.com/problems/combination-sum-ii/" %}

```cpp
set<vector<int>> res;

void getWays(vector<int> &A, int B, int current, vector<int> &output) {
    if(B == 0) {
        res.insert(output);
        return;
    }
    
    for(int i = current; i < A.size(); i++) 
        if(B - A[i] >= 0) {
            output.push_back(A[i]);
            getWays(A, B - A[i], i + 1, output);
            output.pop_back();
        }
}

vector<vector<int> > Solution::combinationSum(vector<int> &A, int B) {
    sort(A.begin(), A.end());
    res.clear();
    
    int current = 0;
    vector<int> output;
    getWays(A, B, current, output);
    vector<vector<int>> v(res.begin(), res.end());
    return v;
}
```

Time Complexity: \$$
