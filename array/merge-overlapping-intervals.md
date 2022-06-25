# ✅ Merge Overlapping Intervals

{% embed url="https://www.interviewbit.com/problems/merge-overlapping-intervals/" %}

{% tabs %}
{% tab title="C++" %}
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

Accepted
{% endtab %}

{% tab title="JS" %}
```javascript
module.exports = { 
    /**
     * Interval: [start, end]
     * 
     * param A: intervals, a list of Intervals
     * return :a list of Intervals
     */
	merge : function(A){        
        A.sort((a, b) => a[0] - b[0])
        
        let res = [A[0]]
        
        for(let interval of A.slice(1)) 
            if(res[res.length - 1][1] < interval[0]) 
                res.push(interval)
            else
                res[res.length - 1][1] = Math.max(res[res.length - 1][1], interval[1])
                
        return res;
	}
};

```
{% endtab %}
{% endtabs %}

Time Complexity: $$O(n\log n)$$​ due to sorting

Space Complexity: $$O(n)$$​ for the result
