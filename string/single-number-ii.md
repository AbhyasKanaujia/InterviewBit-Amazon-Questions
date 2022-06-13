# ⭐ Single Number II

{% embed url="https://www.interviewbit.com/problems/single-number-ii/" %}

<details>

<summary>Thoughts</summary>

* **0:00** This is another variant of the same question that as far as I remember I was able to solve in 30 seconds. Let's see how my time this one takes.&#x20;
* **1:04** I thought I got this one too. I used a **map** to solve this as fast as I could because I couldn't think of any other solution but I got <mark style="color:red;">Memory Limit Exceeded</mark>.  I'll paste it here anyway.
* **3:15** Now I can think in peace since there is no pressure to complete it in an unrealistically small amount of time.
* **7:15** The problem statement clearly says it wants a $$O(n)$$​ solution but I really want to give sorting an attempt. Just for practice. I'll go ahead and do that.
* **14:50** Why am  I finding the sorting approach hard to implement? Am I being careless?&#x20;
* Ok, so it turns out my sorting solution has been accepted.&#x20;
* I will try thinking in terms of bit manipulation. Since this question belongs to that section.
* **18:30** I'm not able to think of a solution. I'll take a hint.&#x20;
* **22:00** Hint couldn't help either so I saw the solution approach. Each number that appears thrice will contribute 3 1s and 0s in all the 32 bits for itself. The number that appears once will only make this contribution once. So the bits that are present $$3x+1$$​ are the bits set by the single number.
* Let me try using an array for this. The solution talks about using a bit-mask but that sounds too complicated.&#x20;
* **31:00** I coded something but it's not working at all. [I'll take it to Online GDB](https://onlinegdb.com/eaQ5I5HiH). last 15 min. Then I'll see the solution.&#x20;
* **42:00** Ok, I'm just not able to solve this. I'll see the solution now.&#x20;
* **48:00** None of the solutions they have posted in the editorial makes sense. I'll find [a YouTube Video](https://www.youtube.com/watch?v=cOFAmaMBVps).&#x20;
* **1:01:00** Tech Dose teaches very well. Wonder why he has so few likes.&#x20;
* **1:09:50** I've got the intuitive solution but I have no will to go for the unintuitive optimal solution. I'll just let it be for now.&#x20;

</details>

### Using Map

```cpp
int Solution::singleNumber(const vector<int> &A) {
    map<int, int> freq;
    for(int x: A)
        freq[x]++;
        
    for(auto p: freq)
        if(p.second == 1)   
            return p.first;
        
    return -1;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(n)$$​

### Using Sorting

```cpp
int Solution::singleNumber(const vector<int> &A) {
    vector<int> B(A.begin(), A.end());
    sort(B.begin(), B.end());
    int i = 0;
    while(i + 1 < A.size()) {
        if(B[i] != B[i + 1])
            return B[i];
        i = i + 3;
    }
    
    if(A.size() == 1)
        return B.front();
    else
        return B.back();
}
```

Time Complexity: $$O(n\log n)$$​

Space Complexity: $$O(n)$$ for duplicating array for sorting

### Counting Set Bits

```cpp
int Solution::singleNumber(const vector<int> &A) {
    int res = 1;
    for(int shift = 0; shift < 32; shift++) {
        int count = 0;
        for(const int &x: A) 
            count += x & (1<<shift);
        
        if(count % 3)
            res = res | (1 << shift);
    }    
}
```
