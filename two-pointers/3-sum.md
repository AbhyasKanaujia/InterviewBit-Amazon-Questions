# ⭐ 3 Sum

{% embed url="https://www.interviewbit.com/problems/3-sum/" %}

<details>

<summary>Thoughts: 1st attempt</summary>

14 June 2022

* **0:00** I've done this question earlier. I can solve this under 5 minutes.&#x20;
* **9:00** I underestimated this question. I am not able to solve it.&#x20;
* I'll  go ahead and see the solution.&#x20;
* **25:00** Neither I'm able to solve it nor am I able to find a good YouTube video for this. [I'll take it to onlineGDB](https://onlinegdb.com/5YnoE7s-t).
* **41:40** I think I've solved it. I'll remove the print statements and try to submit it.&#x20;
* **51:00** I am not able to solve this question. I'll paste my partial solution here.

</details>

### <mark style="background-color:red;">Partially Accepted!</mark>

```cpp
int twoSum(vector<int> &A, int begin, int B) {
    int p1 = begin, p2 = A.size() - 1;
    int minDist = INT_MAX;
    int res;
    while(p1 < p2) {
        int sum = A[p1] + A[p2];
        int dist = abs(B - sum);
        
        if(dist == 0) 
            return sum;        
        
        if(dist < minDist) {
            minDist = dist;
            res = sum;
        }
        
        if(sum - B > 0) 
            p2--;
        else
            p1++;
    }
    return res;
}

int Solution::threeSumClosest(vector<int> &A, int B) {
    int res = 0;
    
    if(A.size() <= 3) {
        for(int i = 0; i < A.size(); i++) 
            res += A[i];
        return res;
    }
    
    int minDist = INT_MAX;
    set<int> s(A.begin(), A.end());
    A.clear();
    for(int x: s)
        A.push_back(x);
        
    
    
    for(int i = 0; i < A.size() - 2; i++) {
        int smallerProblem = B - A[i];
        int sum = twoSum(A, i + 1, smallerProblem) + A[i];
        int dist = abs(sum - B);
        if(dist == 0)
            return sum;
        if(dist < minDist) {
            minDist = dist;
            res = sum;
        }
    }
    return res;
}
```
