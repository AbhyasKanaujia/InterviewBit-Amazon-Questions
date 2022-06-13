# Single Number

{% embed url="https://www.interviewbit.com/problems/single-number/" %}

<details>

<summary>Thoughts</summary>

* **0:00** The name is giving me no hint about what the question is about. Let's see how much time it will take.&#x20;
* **0:35** Solved it in 35 seconds. I missed superman though as I was too excited to write the time in these notes. DONE

</details>

```cpp
int Solution::singleNumber(const vector<int> &A) {
    int res = 0;
    for(int x: A)
        res = res ^ x;
    return res;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(1)$$​
