# ⭐ Subsets II

{% embed url="https://www.interviewbit.com/problems/subsets-ii/" %}

```cpp
set<vector<int> > s;
void getSubset(const vector<int> &A, int current, vector<int> &output) {
    if(current == A.size()) {
        s.insert(output);
        return;
    }
    getSubset(A, current + 1, output);
    output.push_back(A[current]);
    getSubset(A, current + 1, output);
    output.pop_back();
}
vector<vector<int> > Solution::subsetsWithDup(vector<int> &A) {
    s.clear();
    sort(A.begin(), A.end());
    vector<int> output;
    getSubset(A, 0, output);
    vector<vector<int>> res(s.begin(), s.end());
    return res;   
}

```
