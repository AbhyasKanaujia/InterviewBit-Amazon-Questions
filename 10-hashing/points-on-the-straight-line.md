# ⭐ Points on the Straight Line

{% embed url="https://www.interviewbit.com/problems/points-on-the-straight-line/" %}

{% embed url="https://www.youtube.com/watch?v=DTeFavNYkLk" %}

{% tabs %}
{% tab title="C++" %}
```cpp
double getSlope(const int &x1, const int &y1, const int &x2, const int &y2) {
    if(x2 - x1) 
        return (double)(y2 - y1) / (double)(x2 - x1);
    return INT_MAX;        
}

int Solution::maxPoints(vector<int> &A, vector<int> &B) {
    map<double, int> slopeFreq;
    
    int res = 0;
    for(int i = 0; i < A.size() - res - 1; i++) {
        int maxm = 0;
        int slope;
        for(int j = i + 1; j < A.size(); j++) {
            double slope = getSlope(A[i], B[i], A[j], B[j]);
            slopeFreq[slope]++;
            maxm = max(maxm, slopeFreq[slope]);
        }
        slopeFreq.clear();
        res = max(maxm, res);
    }

    return res + 1;
}
```

Not Accepted
{% endtab %}
{% endtabs %}
