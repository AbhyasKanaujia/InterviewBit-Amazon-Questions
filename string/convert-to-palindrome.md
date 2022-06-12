# ⭐ Convert to Palindrome

{% embed url="https://www.interviewbit.com/problems/convert-to-palindrome/" %}

<details>

<summary>Thoughts</summary>

* **5:00** I'm really losing confidence after not being able to solve the last question, so much that I didn't even bother reading the problem statement for this question. I just read the name and assumed that I won't be able to solve it because it might require some fancy algorithm like KMP.&#x20;
* I read the solution and it wasn't so complicated. I coded it but it's giving some errors. I['ll take it to OnlineGDB](https://onlinegdb.com/9iObAqZy8).
* **29:01** It sounds simple but I'm not able to solve it. Here's my attempt:

```cpp
int Solution::solve(string A) {
    int i = 0, j = A.size() - 1;
    while(i < j) // if outermost match then proceed inward
        if(A[i] == A[j])
            i++, j--;
        else { // if mismatched
            return (
                // should still be valid after removal
                // attempt (left || right) removal
                A[i + 1] == A[j] ||
                A[i] == A[j - 1]
            );
        }
        
    return (A.size() & 1);
    // if odd size palindrome
        // then remove middle
    // if even size palidrome
        // non removable
}
```

* I'll go ahead and see the solution.
* **37:00** I was so close but so far from the solution.

</details>

```cpp
bool isPalindrome(const string &str, int i, int j) {
    while(i < j)
        if(str[i++] != str[j--])
            return false;
            
    return true;
}

int Solution::solve(string A) {
    int i = 0, j = A.size() - 1;
    while(i < j) 
        if(A[i] == A[j])
            i++, j--;
        else 
            return isPalindrome(A, i + 1, j) || isPalindrome(A, i, j - 1);            
        
    return (A.size() & 1);
}
```

