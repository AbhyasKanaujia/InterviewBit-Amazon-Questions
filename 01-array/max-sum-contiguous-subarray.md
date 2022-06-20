# ✅ Max Sum Contiguous Subarray

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

Time Complexity: $$O(n)$$​

Space Complexity: $$O(1)$$

## ES6 Solution

```javascript
module.exports = { 
 //param A : array of integers
 //return an integer
    maxSubArray : function(A){
    let sum = A[0];
    let maxSum = A[0];
    
    A.slice(1).map(x => {
        sum = sum < 0 ? x : sum + x;
        maxSum = Math.max(maxSum, sum)
    })
    
    return maxSum;
    }
};
```
