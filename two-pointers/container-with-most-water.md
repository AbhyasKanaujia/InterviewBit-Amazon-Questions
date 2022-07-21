# ⭐ Container With Most Water

{% embed url="https://www.interviewbit.com/problems/container-with-most-water/" %}

<details>

<summary>Thoughts: 1st Attempt</summary>

15th June 2022

* **0:00** I've never seen this question before, and the question has a tag “trick”. It doesn't sound like one of those question I should spend more than 10 minutes on.
* **11:00** I am able to do it on paper. But I'm not able to code it. This is not right. I'll give it a few more minutes.&#x20;
* **24:00** OK, I was able to code what I did on paper.
* **25:00** I'll see the solution now.
* **33:00** Watching [this YouTube Video](https://www.youtube.com/watch?v=ZHQg07n\_tbg).&#x20;
*

</details>

### Brute Force: Not Accepted

```cpp
int Solution::maxArea(vector<int> &A) {
    int res = INT_MIN;
    if(A.size() <= 1)
        return 0;
    for(int size = 1; size <= A.size(); size++) 
        for(int start = 0; start < A.size() - size; start++) {
            int height = INT_MAX;
            for(int i = start; i <= start + size; i++)
                height = min(height, A[i]);
            res = max(res, height * size);
        }
    return res;
}
```

### Using two poiners

```cpp
int Solution::maxArea(vector<int> &A) {
    if(A.size() <= 1)
        return 0;
    long long res = 0;
    long long p1 = 0, p2 = A.size() - 1;
    while(p1 < p2) {
        res = max(res, (p2 - p1) * min((long long)A[p1], (long long)A[p2]));
        if(A[p1] < A[p2])
            p1++;
        else
            p2--;
    }
    
    return res;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(1)$$​
