# ⭐ Largest Rectangle in Histogram

{% embed url="https://www.interviewbit.com/problems/largest-rectangle-in-histogram/" %}

```cpp
int Solution::largestRectangleArea(vector<int> &A) {
    stack<int> smallerIndex;
    
    deque<int> leftSmaller(A.size(), 0), rightSmaller(A.size(), A.size() - 1);
    
    // get left smaller
    for(int i = 0; i < A.size(); i++) {
        while(!smallerIndex.empty() && A[smallerIndex.top()] >= A[i])
            smallerIndex.pop();
            
        if(!smallerIndex.empty())
            leftSmaller[i] = smallerIndex.top() + 1;
            
        smallerIndex.push(i);
    }
    
    while(!smallerIndex.empty())
        smallerIndex.pop();
    
    // get right smaller 
    for(int i = A.size() - 1; i >= 0; i--) {
        while(!smallerIndex.empty() && A[smallerIndex.top()] >= A[i])
            smallerIndex.pop();
            
        if(!smallerIndex.empty()) 
            rightSmaller[i] = smallerIndex.top() - 1;
            
        smallerIndex.push(i);
    }
    
    int maxArea = INT_MIN;
    
    for(int i = 0; i < A.size(); i++) 
        maxArea = max(maxArea, (rightSmaller[i] - leftSmaller[i] + 1) * A[i]);
    
    return maxArea;
}

```
