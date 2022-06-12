# Count And Say

{% embed url="https://www.interviewbit.com/problems/count-and-say/" %}

<details>

<summary>Thoughts</summary>

* So it took me 5 minutes to make a successful submission.&#x20;
* I still think this is not the most optimal solution.
* This one's a $$O(n^2)$$​ solution. I'll just go ahead and see the actual solution.&#x20;
* This is it. My solution is clearer and lighter than the one provided.&#x20;

</details>

```cpp
string getNextSequence(const string &num) {
    int i = 0; 
    string res = "";
    while(i < num.size()) {
        char digit = num[i];
        int count = 0;
        while(i < num.size() && num[i] == digit) 
            i++, count++;
        
        res += to_string(count) + digit;
    }
    
    return res;
}

string Solution::countAndSay(int A) {
    string res = "1";
    for(int i = 1; i < A; i++) 
        res = getNextSequence(res);
        
    return res;
}
```

Time Complexity: $$O(n^2)$$​

Space Complexity: $$O(n)$$ for the result

