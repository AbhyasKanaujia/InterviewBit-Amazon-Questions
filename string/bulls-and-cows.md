# Bulls and Cows

{% embed url="https://www.interviewbit.com/problems/bulls-and-cows/" %}

<details>

<summary>Thoughts</summary>

* **0:00** Bulls and Cows, :rofl: [the game I made years ago](https://github.com/AbhyasKanaujia/BullsAndCows\_Game) in a course from Udemy.
* I can only think of a brute force solution where I match each character.&#x20;
* I can also think of sorting. Let me try the brute force once.&#x20;
* **26:00** Brute Force solution got accepted.&#x20;
* I feel like it's ok to tell the interviewer your brute force solution. Sometimes the brute force solution is the most optimal one. If it is then they will be satisfied. If not they will ask you to optimize it.&#x20;
* Here I have the solution to look at to know if there exists an optimal solution. But in an interview, I have to start with brute force. Because I don't know if what I'm calling brute force is the optimal solution. &#x20;
* Let me see the time complexity of the solution.
* Turns out it wasn't a brute force solution. It was an $$O(n)$$​ solution.&#x20;

</details>

### Brute Force Approach

1. Mark and count all `bulls` i.e. matched chars and indices.&#x20;
2. Mark and count all those not marked as `bulls`

```cpp
// function to count number of bulls and mark each
// bull char in input as used. 
int getBullsAndMark(string &A, const string &B) {
    int count = 0;
    for(int i = 0; i < A.size(); i++)    
        if(A[i] == B[i]) {
            A[i] = 'b';
            count++;
        }
        
    return count;
}

// function to find and mark ch in A as used as cow
bool MarkIfUnused(string &A, const char &ch) {
    for(int i = 0; i < A.size(); i++)
        if(A[i] == ch) {
            A[i] = 'c';
            return true;
        }
        
        return false;
}

string Solution::solve(string A, string B) {
    int bulls = getBullsAndMark(A, B), cows = 0;
    
    // if unused cow found then count for each
    // ununsed in B 
    // Use A[i] == 'b' => B[i] == 'b'
    for(int i = 0; i < B.size(); i++) 
        if(A[i] != 'b' && MarkIfUnused(A, B[i]))
            cows++;
            
    return to_string(bulls) + "A" + to_string(cows) + "B";    
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(1)$$​
