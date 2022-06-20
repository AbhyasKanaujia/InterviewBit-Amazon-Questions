# Palindrome Partitioning

{% embed url="https://www.interviewbit.com/problems/palindrome-partitioning/" %}

```cpp
vector<vector<string>> res;

bool isPalindrome(string str) {
    int i = 0, j = str.size() - 1;
    while(i < j)   
        if(str[i++] != str[j--])
            return false;
    return true;
}

void getWays(const string A, int current, vector<string> output) {
    if(current == A.length()) {
        res.push_back(output);
        return;
    }
    
    for(int i = current; i < A.size(); i++) 
        if(isPalindrome(A.substr(current, i - current + 1))) {
            output.push_back(A.substr(current, i - current + 1));
            getWays(A, i + 1, output);
            output.pop_back();
        }
}

vector<vector<string> > Solution::partition(string A) {
    res.clear();
    vector<string> output;
    getWays(A, 0, output);
    return res;
}
```
