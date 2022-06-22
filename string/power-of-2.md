# Power of 2

{% embed url="https://www.interviewbit.com/problems/power-of-2/" %}

<details>

<summary>Thoughts</summary>

* **0:00** This sounds like a super easy question that I should be able to solve in 2 minutes. But since this question is in the string section, so I don't think it's going to be that simple. I'll try it once.&#x20;
* **10:00** It's not simple at all. The question asks to check if the given number, which is very huge and in a string, is a power of two or not.&#x20;
* So it's very similar to the factorial problem where we need to do multiplication manually.&#x20;
* I'm getting some errors. [I'll take it to OnlineGDB](https://onlinegdb.com/8wvor7Y6V).
* **25:00** Turns out I messed up in the multiplication function. I forgot to reverse the result of the multiplication.&#x20;
* Also, I forgot some edge cases.
* **28:00** Done from my side. Let me take a loot at the given solution.&#x20;
* Their solution is not even following the constraint. They are converting the string to `int` and then doing the basic bit manipulation technique.&#x20;
* This reminds me that I have forgotten the bit manipulation technique to check for the power of two. Time to see notes.&#x20;

</details>

```cpp
int comp(string B, string A){
    if(B.size() == A.size())
        return (B < A ? -1 : B > A ? 1 : 0);
    return (B.size() < A.size() ? -1 : 1);
}

string timesTwo(string B) {
    reverse(B.begin(), B.end());
    int carry = 0;
    string res = "";
    int i = 0; 
    while(i < B.size()) {
        int prod = (B[i] - '0') * 2 + carry;
        res.push_back((prod % 10) + '0');
        carry = prod / 10;
        i++;
    }
    
    while(carry) {
        res.push_back((carry % 10) + '0');
        carry /= 10;
    }
    
    reverse(res.begin(), res.end());
    return res;
}

int Solution::power(string A) {
    // edge case
    if(A == "1" || A[0] == '-')
        return 0;
    string B = "1";
    while(comp(B, A) == -1) 
        B = timesTwo(B);
        
    return (comp(B, A) == 0);
}
```

Time Complexity: $$(n \log n)$$​

Space Complexity: $$O(n)$$​ for products of $$2$$​.

Edge Cases:&#x20;

* You initialized `res = 1` But is $$1$$​ being equal to given number a valid case?
* What if the input is negative?
