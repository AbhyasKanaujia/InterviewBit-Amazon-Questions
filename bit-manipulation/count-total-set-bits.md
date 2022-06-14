# ⭐ Count Total Set Bits

{% embed url="https://www.interviewbit.com/problems/count-total-set-bits/" %}
Given a positive integer **A**, the task is to count the total number of set bits in the binary representation of all the numbers from **1** to **A**.
{% endembed %}

<details>

<summary>Thoughts</summary>

* **0:00** It's marked as a hard problem.
* **5:00** I observed that for numbers from 1 - 15 each position has 8 set bits. Let me [write a program](https://onlinegdb.com/phWbU1te\_) for making observations.&#x20;
* **14:20** I'm sick of C++ being so less user-friendly when it comes to the user-facing part of it. I want to print a table and I need to program a whole lot. I'll try doing it in JavaScript this time.&#x20;
* **38:51** JavaScript `console.table()` is working beautifully. Just that I don't know enough JavaScript to utilize it fully. This is wasting more time for me than helping me see patterns. I'll just do it the old way using pen and paper. \
  ![](../.gitbook/assets/image.png)
* **48:00** I see some patterns but those are not very helpful. I'll just see the solution now I've spent too much time on this.&#x20;
* **49:00** I give the brute force approach a try before seeing the solution.&#x20;
* **57:00** I'll see the solution.
* **1:08:10** I don't understand their solution. I'll watch [a YouTube Video](https://www.youtube.com/watch?v=g6OxU-hRGtY).&#x20;
* **1:15:00** Pepcoding teaches really well.&#x20;
* **1:42:00** Finally Done.

</details>

### Brute Force Solution&#x20;

```cpp
int countSetBits(const int &num) {
    int res = 0;
    for(int i = 0; i < 32; i++)
        res += ((num & (1 << i)) != 0);
        
    return res;
}
 
int Solution::solve(int A) {
    int res = 0;
    for(int i = 1; i <= A; i++)
        res += countSetBits(i);
        
    return res;
}
```

Time Complexity: $$O(n^2)$$​

Space Complexity: $$O(1)$$​

### Optimal Solution

{% embed url="https://www.youtube.com/watch?v=g6OxU-hRGtY" %}

```cpp
long long largestPower(long long A) {
    int res = 0;
    while((1 << res) <= A)
        res++;
        
    return res - 1;
}

long long getCount(long long A) {
    if(A == 0)
        return 0;
        
    long long x = largestPower(A);
    
    return x * (1 << (x - 1)) + A - (1 << x) + 1 + getCount(A - (1 << x));
}

int Solution::solve(int A) {
    long long res = getCount(A);
    return res % 1000000007;
}

```
