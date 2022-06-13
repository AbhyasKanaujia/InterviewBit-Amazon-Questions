# Reverse Bits

{% embed url="https://www.interviewbit.com/problems/reverse-bits/" %}
Reverse the bits of an **32** bit unsigned integer A.
{% endembed %}

<details>

<summary>Thougts</summary>

* **0:00** Sounds like an easy question I should be able to solve in 2 minutes.&#x20;
* **7:30** Ok, it was easy enough. DONE.

</details>

```cpp
inline bool isSet(const unsigned int &A, const int &pos) {
    return A & (1 << (pos - 1));
}

inline void setBit(unsigned int &num, const int &pos) {
    num = num | (1 << (32 - pos));
}

unsigned int Solution::reverse(unsigned int A) {
    unsigned int res = 0;
    
    for(int pos = 1; pos <= 32; pos++) 
        if(isSet(A, pos))
            setBit(res, pos);
            
    return res;
}
```

Short Version:

```cpp
unsigned int Solution::reverse(unsigned int A) {
    unsigned int res = 0;
    
    for(int pos = 1; pos <= 32; pos++) 
        if(A & (1 << (pos - 1)))
            res = res | (1 << (32 - pos));
            
    return res;
}
```

Time Complexity: $$O(1)$$

Space Complexity: $$O(1)$$​
