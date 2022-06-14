# ⭐ Palindromic Binary Representation

{% embed url="https://www.interviewbit.com/problems/palindromic-binary-representation/" %}

<details>

<summary>Thoughts</summary>

14th June 2022

* **0:00** I'm having lots of difficulty in the Bit Manipulation part. Should I visit the LeetCode Discuss section regarding this? I'll give it a try.
* I visited the leet code study guide section and I can see that there's not much that I don't know. It's just that these are standard problems with standard solutions that I need to have seen to be able to solve. No gap in my knowledge as far as I can see.&#x20;
* **4:00** It's a hard problem. I'll just go straight to the solution. It's probably very convoluted and not reachable on my own.&#x20;
* **6:00** I'll just go find [a YouTube video](https://www.youtube.com/watch?v=QYoWR8hDCyQ). Their solution rarely makes sense to me.&#x20;
* **36:00** One of the best explanations on the internet is from pepcoding.&#x20;
* **42:30** The solution is clear to me now. I'll code it.&#x20;
* **47:00** Done. Need to dry run properly during revision.&#x20;

</details>

{% embed url="https://youtu.be/QYoWR8hDCyQ" %}

```cpp
int getReverse(int n) {
    int rev = 0;
    
    while(n) {
        int lb = n & 1;
        
        rev |= lb;
        n >>= 1;
        rev <<= 1;
    }
    
    rev >>= 1;
    
    return rev;
}

int Solution::solve(int n) {
    int count = 1;
    int len = 1;
    
    while(count < n) {
        len++;
        int elementsForThisLen = (1 << (len - 1) / 2);
        count += elementsForThisLen;
    }
    
    count -= (1 << (len - 1) / 2);
    int offset = n - count - 1;
    
    int ans = (1 << (len - 1));
    ans |= (offset << (len / 2));
    
    int valForReverse = (ans >> (len / 2));
    int rev = getReverse(valForReverse);
    
    ans |= rev;
    
    return ans;
}

```
