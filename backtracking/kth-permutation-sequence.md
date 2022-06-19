# ⭐ Kth Permutation Sequence

{% embed url="https://www.interviewbit.com/problems/kth-permutation-sequence/" %}

## For Small input size where factorial calculation is possible

{% embed url="https://www.youtube.com/watch?v=wT7gcXLYoao" %}

```cpp
string Solution::getPermutation(int A, int k) {
    vector<int> nums(A);
    for(int i = 0; i < A; i++)
        nums[i] = i + 1;
    string ans = "";
    int fact = 1;
    for(int i = 1; i < A; i++)
        fact *= i;
        
    k = k - 1;
        
    while(true) {
        ans = ans + to_string(nums[k / fact]);
        nums.erase(nums.begin() + k / fact);
        if(nums.size() == 0)
            break;
        k = k % fact;
        fact = fact / nums.size();
    }
    return ans;
}
```

## Any size input

```cpp
int fact(int n) {
    if(n > 12)
        return INT_MAX;
    if(n < 1)
        return 1;
        
    return n * fact(n - 1);
}

void solve(int A, int B, vector<int> &v, string &ans) {
    if(A == 1) {
        ans += to_string(v.back());
        return;
    }
    
    int f = fact(A - 1);
    int index = B / f;
    if(B % f == 0)
        index--;
        
    ans += to_string(v[index]);
    v.erase(v.begin() + index);
    B -= f * index;
    solve(A - 1, B, v, ans); 
}

string Solution::getPermutation(int A, int B) {
    vector<int> v;
    for(int i = 1; i <= A; i++)
        v.push_back(i);
        
    string ans = "";
    solve(A, B, v, ans);
    return ans;
}
```
