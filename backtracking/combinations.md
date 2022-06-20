# Combinations

{% embed url="https://www.interviewbit.com/problems/combinations/" %}

```cpp
vector<vector<int>> res;

void getWays(int start, const int &end, const int &len, vector<int> &output) {
    if(output.size() == len) {
        res.push_back(output);
        return;
    }   
    
    for(int i = start; i <= end; i++) {
        output.push_back(i);
        getWays(i + 1, end, len, output);
        output.pop_back();
    }
}

vector<vector<int> > Solution::combine(int A, int B) {
    res.clear();
    if(B > A)
        return res;
    int start = 1;
    int end = A;
    int len = B;
    vector<int> output;
    getWays(start, end, len, output);
    return res;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(^AC_B)$$ for storing result​
