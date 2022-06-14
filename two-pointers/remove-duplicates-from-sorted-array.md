# Remove Duplicates from sorted Array

{% embed url="https://www.interviewbit.com/problems/remove-duplicates-from-sorted-array/" %}
Given a sorted array **A** consisting of duplicate elements.\
Your task is to remove all the duplicates and return a sorted array of distinct elements consisting of all distinct elements present in **A**.
{% endembed %}



<details>

<summary>Thoughts: 1st attempt</summary>

14 June 2022

* **0:00** I am feeling extremely insecure. I wasn't able to any question today. Let me try this last question for today.&#x20;
* **2:30** Why would they call this an easy question?
* **4:20** I'll loot at the solution.
* **6:30** I didn't even read the question properly. Why was I sorting it? Its already sorted?? I just read in-place and assumed it's a sorting question.&#x20;
* **8:30** So it's a remove duplicate question. Let me give it a try again.
* **10:20** Solved. It really was an easy question after all. Loosing confidence will take me no where.&#x20;

</details>

```cpp
int Solution::removeDuplicates(vector<int> &A) {
    int place = 0;
    int find = 1;
    while(find < A.size()) {
        if(A[find] != A[place]) {
            A[place + 1] = A[find];
            place++;
        }
        find++;
    }
    return place + 1;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(1)$$​
