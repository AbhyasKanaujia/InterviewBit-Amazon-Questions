# Merge Intervals

{% embed url="https://www.interviewbit.com/problems/merge-intervals/" %}

<details>

<summary>Logic</summary>

1. For every `interval` in `intervals`
   1. If it comes before the `newInterval` with no overlap: `current.end < newInterval.start`
      1. Push `current` into the `result` vector
   2. If `newInterval` comes before the `current` interval with no overlap: `current.start > newInterval.end`
      1. Push  `newInterval` into the `result` vector
      2. `current` is the new `newInterval`
   3. If both conditions are false then definitely there has been an overlap
      1. Merge the `current` interval to `newInterval`
2. In the end, `newInterval` will be left&#x20;
   1. Push it into the `result` vector

</details>

<details>

<summary>Code</summary>

```cpp
vector<Interval> Solution::insert(vector<Interval> &intervals, Interval newInterval) {
    vector<Interval> res;

    for(Interval test: intervals) 
        // New Interval comes after Test with no overlap
        if(newInterval.start > test.end)        
            // insert Test
            res.push_back(test);    
        // new interval comes before thest with no overlap                   
        else if(test.start > newInterval.end) { 
            // insert New Interval
            res.push_back(newInterval);  
            // Put Test into New Interval           
            newInterval = test;    
        // any other case of over lap                 
        } else
            // merge Test with New Interval                            
            newInterval = Interval(min(test.start, newInterval.start), max(test.end, newInterval.end));

    res.push_back(newInterval);
    return res;
}
```

</details>

<details>

<summary>Compleixty</summary>

Time Complexity: $$O(n)$$​

Space Complexity: $$O(n)$$​

</details>
