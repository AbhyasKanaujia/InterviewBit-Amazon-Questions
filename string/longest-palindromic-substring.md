# ⭐ Longest Palindromic Substring

{% embed url="https://www.interviewbit.com/problems/longest-palindromic-substring/" %}

<details>

<summary>Thoughts</summary>

* It says **substring** so probably I need a **sliding window**.&#x20;
* It also says **palindrome** so probably I need the **two-pointer**.&#x20;
* But then using both of these will make it a brute force solution.&#x20;
* I'll generate every substring and check for palindrome using the two-pointer approach.
* I'll just go ahead and code the brute force one once.
* 28:00 Ok so the solution that I assumed to be a <mark style="color:green;">brute force one got accepted</mark> as a valid solution. I'll paste it here and **see what the actual solution** is.
* 31:00 Watching [Neet Code's Explanation](https://www.youtube.com/watch?v=XYQecbcd6\_c)
* What's the time Complexity of my current solution?
* Neet Code is pretty lazy with his code. Don't pick his ways. Be strong. Be hard working.&#x20;
* 42:00 Video Watched. Start Coding.
* 51:00 Coded and got accepted. I'll paste the code here.&#x20;
* 53:00 Done. I'll add this method to the [formula list](https://abhyas-kanaujia.gitbook.io/lb-dsa-notes-and-homework-abhyas/formula-list#palindrome-test).

</details>

### Brute Force

```cpp
inline bool isPlaindrome(string::iterator begin, string::iterator end) {
    while(begin < end) 
        if(*(begin++) != *(end--))
            return false;
            
    return true;
}
string Solution::longestPalindrome(string A) {
    int longest = INT_MIN;
    string res = "";
    for(int i = 0; i < A.size(); i++)
        for(int j = i; j < A.size(); j++)
            if(j - i + 1 > longest) 
                if(isPlaindrome(A.begin() + i, A.begin() + j)) {
                    res = A.substr(i, j - i + 1);
                    longest = j - i + 1;
                }
    return res;
}
```

Time Complexity: $$O(n^3)$$

Where `isPalindrome(str)` takes $$O(n)$$​ time and generating all the substrings take $$O(n^2)$$​ time.

Space Complexity: $$O(n)$$​ for the result.

### Efficient Solution

{% embed url="https://www.youtube.com/watch?v=XYQecbcd6_c" %}

```cpp
void getLargePalindromAt(const string &str, int left, int right, int &resLen, string &res) {
    while(left >= 0 && right < str.size() && str[left] == str[right]) {
        if(right - left + 1 > resLen) {
            resLen = right - left + 1; 
            res = str.substr(left, right - left + 1);
        }
        left--, right++;
    }
}

string Solution::longestPalindrome(string A) {
    string res = "";
    int resLen = 0;
    for(int center = 0; center < A.size(); center++){
        int left = center, right = center;
        getLargePalindromAt(A, left, right, resLen, res);
        left = center, right = center + 1;
        getLargePalindromAt(A, left, right, resLen, res);
    }
        
    return res;
}

```

Time Complexity: $$O(n^2)$$​

Space Complexity: $$O(n)$$​ for the result

Logic: Assume each letter as a centre of a palindrome and expand outward while checking if it is a palindrome.

Edge Case: Even Length palindrome.
