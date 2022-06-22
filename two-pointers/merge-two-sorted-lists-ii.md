# Merge Two Sorted Lists II

{% embed url="https://www.interviewbit.com/problems/merge-two-sorted-lists-ii/" %}
Given two sorted integer arrays A and B, merge B into A as one sorted array.
{% endembed %}

<details>

<summary>Thoughts: 1st attempt</summary>

14 June 2022

* **0:00** The name of the question tells me it's going to be an easy problem, but the “II” in its name tells me otherwise. Let me give it a try.&#x20;
* **1:29** I wanted to do it under an unrealistic amount of time, so I cheated and used sorting. It is a solution anyway.&#x20;
* **2:58** OK, now I'll think of better ways to do it besides sorting. I still have lots of time. I'll spend about 30 minutes on this.&#x20;
* **8:00** I solved it using a third vector. I think that's it from my side. I'll look at the solution.&#x20;
* **16:00** My two pointer solution was the most optimal one. Great.&#x20;

</details>

### Using Sorting

```cpp
void Solution::merge(vector<int> &A, vector<int> &B) {
    for(int x: B)
        A.push_back(x);
        
    sort(A.begin(), A.end());       
}
```

Time Complexity: $$O(n\log n)$$​

Space Complexity: $$O(m+n)$$

### Using a third vector and two pointers

```cpp
void Solution::merge(vector<int> &A, vector<int> &B) {
    vector<int> res;
    
    int p1 = 0, p2 = 0;
    while(p1 < A.size() && p2 < B.size())
        if(A[p1] < B[p2])
            res.push_back(A[p1++]);
        else
            res.push_back(B[p2++]);
            
    while(p1 < A.size())
        res.push_back(A[p1++]);
        
    while(p2 < B.size())
        res.push_back(B[p2++]);
        
    A.resize(res.size());
    for(int i = 0; i < res.size(); i++)
        A[i] = res[i];
}
```

Time Complexity: $$O(m + n)$$​

Space Complexity: $$O(m + n)$$​
