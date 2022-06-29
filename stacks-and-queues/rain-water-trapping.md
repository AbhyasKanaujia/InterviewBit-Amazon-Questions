# Rain Water Trapping

{% embed url="https://www.interviewbit.com/problems/rain-water-trapped/" %}

```cpp
int Solution::trap(const vector<int> &A) {
    deque<int> maxLeft = {A.front()};
    deque<int> maxRight = {A.back()};
    
    for(int i = 1; i < A.size(); i++) 
        maxLeft.push_back(max(maxLeft.back(), A[i]));
    
    for(int i = A.size() - 2; i >= 0; i--) 
        maxRight.push_front(max(maxRight.front(), A [i]));
        
    int totalWaterTrapped = 0;
    
    for(int i = 1; i < A.size() - 1; i++) 
        totalWaterTrapped += min(maxLeft[i], maxRight[i]) - A[i];
        
    return totalWaterTrapped;    
}
```
