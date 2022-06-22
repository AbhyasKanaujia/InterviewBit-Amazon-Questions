# 🚧 KMP: Minimum Characters  Required to Make a String Palindromic

{% embed url="https://www.interviewbit.com/problems/minimum-characters-required-to-make-a-string-palindromic/" %}

<details>

<summary>Thoughts</summary>

* **0:00** The name of the questions sounds like one of those that I clearly won't be able to solve on my own. I'll just give it a try once and see if I should go straight to the solution.&#x20;
* **36:00** I spent a lot more time than I wanted to. I have a solution that should work but it's giving the wrong answer. [Time to take it to OnlineGDB](https://onlinegdb.com/hMadqrAus).
* **45:00** So the problem was that I read the question wrong and thought that we can insert characters at both the beginning and the end. Let's see if it will work now that I know this.&#x20;
* Ok, so my solution was correct but not optimal. I'm surprised I was able to solve this at all. I'll paste it here as a brute-force solution and see the provided solution.&#x20;
* **50:00** According to the hint, I need to learn KMP. I'll go ahead and watch a video on that.
* **54:00** According to Need Code, KMP is a very very very hard problem. I don't have time right now as I'm behind schedule, so i'll defer it for now and move to the next question.&#x20;

</details>

### Brute Force

The `getPalindromeAt()` is the same as the one used in the [Longest Palindrome Substring](longest-palindromic-substring.md#efficient-solution) solution.&#x20;

```cpp
int getMinRes(pair<int, int> palindrome, int size, int res) {
    if(palindrome.first == 0)
        res = min(res, size - palindrome.second - 1);
    // if insertion at end was allowed then
    // if(palindrome.second == size - 1)
    //     res = min(res, palindrome.first);
    
    return res;
}
pair<int, int> getPalindromeAt(const string &A, int begin, int end) {
    pair<int, int> res;
    while(begin >= 0 && end < A.size()) {
        if(A[begin] == A[end])
            res.first = begin, res.second = end;
        else    
            break;
        begin--, end++;
    }
    return res;    
}

int Solution::solve(string A) {
    pair<int, int> palindrome;
    int res = INT_MAX;
    for(int i = 0; i < A.size(); i++) {
        palindrome = getPalindromeAt(A, i, i);
        res = getMinRes(palindrome, A.size(), res);
        
        if(i + 1 < A.size()) {
            palindrome = getPalindromeAt(A, i, i + 1);
            res = getMinRes(palindrome, A.size(), res);    
        }
    }
    return res;
}

```
