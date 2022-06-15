# ⭐ Max Continuous Series of 1s

{% embed url="https://www.interviewbit.com/problems/max-continuous-series-of-1s/" %}

<details>

<summary>Thoughts</summary>

* This one can be solved with Kaden's. But it's in two pointers category. So maybe not. Let's see.&#x20;

</details>

{% embed url="https://www.youtube.com/watch?v=QPfalDbqa4A" %}

The video doesn't cover the case where first few elements are zeros. This code handles this too.

```cpp
vector<int> getRes(int left, int right) {
    vector<int> res;
    for(int i = left; i <= right; i++)
        res.push_back(i);
    return res;
}

vector<int> Solution::maxone(vector<int> &A, int B) {
    int left = -1, right = 0, zeros = (A[0] == 0);
    int maxLen = 1;
    int resLeft, resRight;
    vector<int> res;
    
    // find first valid index
    while(zeros > B && right < A.size()) {
        if(A[++right] == 0)
            zeros++;
        if(A[++left] == 0)
            zeros--;
    }
    
    while(right + 1< A.size()) {
        right++;
        
        if(A[right] == 0)
            zeros++;
            
        if(zeros <= B){
            if((right - left) > maxLen) {
                maxLen = right - left;
                resLeft = left + 1, resRight = right;
            }
        } else {
            left++;
            if(A[left] == 0)
                zeros--;
        }
    }

    return getRes(resLeft, resRight);
}
```
