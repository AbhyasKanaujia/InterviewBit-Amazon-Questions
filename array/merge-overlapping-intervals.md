# Merge Overlapping Intervals

{% embed url="https://www.interviewbit.com/problems/merge-overlapping-intervals/" %}

```cpp
bool comp(const Interval i1, const Interval i2) {
    return i1.start < i2.start;
}

vector<Interval> Solution::merge(vector<Interval> &A) {
    sort(A.begin(), A.end(), comp);
    vector<Interval> res = {A[0]};

    for(int i = 1; i < A.size(); i++) {
        if(res.back().end < A[i].start)
            res.push_back(A[i]);
        else 
            res.back().end = max(res.back().end, A[i].end);
    }
    return res;
}
```
