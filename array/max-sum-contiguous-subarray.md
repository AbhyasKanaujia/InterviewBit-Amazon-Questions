# Max Sum Contiguous Subarray

{% embed url="https://www.interviewbit.com/problems/max-sum-contiguous-subarray/" %}

### Kaden's Algorithm

```cpp
int Solution::maxSubArray(const vector<int> &A) {
    int maxSum = INT_MIN;
    int sum = 0;

    for(int x: A) {
        if(sum < 0)
            sum = x;
        else 
            sum += x;
        
        maxSum = max(maxSum, sum);
    }     
    return maxSum;
}
```
