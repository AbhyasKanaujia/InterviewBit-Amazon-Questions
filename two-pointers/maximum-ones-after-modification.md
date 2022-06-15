# ⭐ Maximum Ones After Modification

{% embed url="https://www.interviewbit.com/problems/maximum-ones-after-modification/" %}

```cpp
int Solution::solve(vector<int> &A, int B) {
    int left = -1, right = 0, zeros = (A[0] == 0);
    int maxLen = 1;
    
    while(zeros > B && right > A.size()) {
        if(A[++right] == 0)
            zeros++;
        if(A[++left] == 0)
            zeros--;
    }
    
    while(right + 1 < A.size()) {
        right++;
        
        if(A[right] == 0)
            zeros++;
        
        if(zeros <= B) 
            if(right - left > maxLen)                                      
                maxLen = right - left;
        
        while (zeros > B) {
            left++;
            if(A[left] == 0)
                zeros--;
        }
    }
    
    return maxLen;
}
```
