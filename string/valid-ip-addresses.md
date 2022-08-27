# ⭐ Valid IP Addresses

{% embed url="https://www.interviewbit.com/problems/valid-ip-addresses/" %}

```cpp
void getWays(const string &A, set<string> &s, int start = 0, int part = 0, string output= "") {
    if(part == 4) {
        if(start == A.size()) {
            output.pop_back();
            s.insert(output);
        }
        return;
    }
    
    for(int end = start; end < min(start + 3, (int)A.size()); end++) {
        string sub = A.substr(start, end - start + 1); 
        if(stoi(sub) < 256 && (start == end || sub[0] != '0'))
            getWays(A, s, end + 1, part + 1, output + sub + ".");
    }
}
vector<string> Solution::restoreIpAddresses(string A) {
    vector<string> res;
    
    if(A.size() > 12)
        return res;
        
    set<string> s;
    getWays(A, s);
    
    
    for(auto x: s)
        res.push_back(x);
        
    return res;
}
```

## Edge Cases

* `size <= 3`
* `index+size <= A.size()`
* `stoi(sub)<256 && (size == 1 || sub[0] != '0')`
