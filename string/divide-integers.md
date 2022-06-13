---
cover: >-
  https://images.unsplash.com/photo-1496694048509-8e8d567dd69d?crop=entropy&cs=tinysrgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHwxMHx8ZGl2aWRlfGVufDB8fHx8MTY1NTEzNjU1Mw&ixlib=rb-1.2.1&q=80
coverY: 0
---

# ⭐ Divide Integers

{% embed url="https://www.interviewbit.com/problems/divide-integers/" %}

<details>

<summary>Thoughts</summary>

* **0:00** Never heard of this question. Let's see how it goes. I assume I can solve this in 30 min.
* **2:40** I simply subtracted the second number from the first one until it becomes less than the second. It is not able to handle negative inputs.&#x20;
* **5:33** I handled negative numbers using a `sign` variable. But now I'm getting an error for `INT_MAX` as input. I should take it to OnlineGDB.&#x20;
* **10:30** I'm using `long long` datatype now. But it's being really slow. Let me give it a try once.&#x20;
* As expected I'm getting a TLE. I'll paste my solution for positive input here and see the solution.&#x20;
* **22:00** I saw the hint. it talks about using bit manipulation to find the answer but I'm not thinking in terms of bit manipulations at all. This tells me that I'm nowhere close to the correct solution. I'll see the solution approach now.&#x20;
* **27:00** The solution tells me to use bit-level division. But I forgot how to do this. Sorry, Dipesh Sir.&#x20;
* I'll see the complete solution now.
* **34:00** The solution is too cryptic. I'll watch [a YouTube video for this](https://youtu.be/X2Ko1Jt9bL4).&#x20;
* **50:00** It was a really bad video. I'll try to dry-run his code and see what's going on.&#x20;
* **59:00** Can't believe I'm spending almost an hour on a single question. The solution is pretty clear now. I'll try to code it once.&#x20;
* **1:00:15** I am not able to solve this question. I will paste my best attempt here.

</details>

<details>

<summary>Wrong Attempts</summary>

Only works for positive input:&#x20;

```cpp
int Solution::divide(int A, int B) {    
    if(B == 0)
        return INT_MAX;
    int res = 0;
    while(A >= B) {
        res++;
        A -= B;
    }
    
    return res;
}
```

Handles negative numbers by using `abs()` but fails for `A = INT_MIN` as abs(A) is again `INT_MIN` due to rounding.&#x20;

```cpp
int Solution::divide(int A, int B) {
    int sign = 1;
    if(A < 0)
        sign *= -1;
    if(B < 0)
        sign *= -1;
        
    A = abs(A);
    B = abs(B);
    if(B == 0)
        return INT_MAX;
    int res = 0;
    while(A >= B) {
        res++;
        A -= B;
    }
    
    return res;
}
```

Using bit maniputaion

```cpp
int Solution::divide(int A, int B) {
    long long a = A, b = B;
    long long sign = 1;
    if(a < 0) sign = -sign, a = -a;
    if(b < 0) sign = -sign, b = -b;
    
    long long ans = 0, temp = 0;
    for(int i = 31; i >= 0; i--)
        if(temp + (b << i) <= a) {
            temp = temp + (b << i);
            ans += (1ll << i);
        }
        
    if(ans > INT_MAX or ans < INT_MIN) return INT_MAX;
    
    return (sign == -1) ? -ans : ans;
}

```

</details>
