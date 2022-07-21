# ⭐ Meeting rooms

{% embed url="https://www.interviewbit.com/problems/meeting-rooms/" %}

{% embed url="https://www.youtube.com/watch?v=FdzJmTCVyJU" %}

```cpp
int Solution::solve(vector<vector<int> > &A) {
    vector<int> startTimes;
    vector<int> endTimes;
    
    for(vector<int> meetings: A) {
        startTimes.push_back(meetings[0]);
        endTimes.push_back(meetings[1]);
    }
    
    sort(startTimes.begin(), startTimes.end());
    sort(endTimes.begin(), endTimes.end());
    
    int p1 = 0, p2 = 0;
    
    int count = 0, maxCount = 0;
    while(p1 < A.size()) {
        if(startTimes[p1] < endTimes[p2]) {
            count++;
            p1++;
        } else {
            count--;
            p2++;
        }
            
        maxCount = max(maxCount, count);
    }
    
    return maxCount;
}
```

