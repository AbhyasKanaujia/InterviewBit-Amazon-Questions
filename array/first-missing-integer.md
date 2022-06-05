# First Missing Integer

{% embed url="https://www.interviewbit.com/problems/first-missing-integer/" %}

### Brute Force

<details>

<summary>Code</summary>

```cpp
int Solution::firstMissingPositive(vector<int> &A) {
    for(int i = 1; i <= A.size() + 1; i++) {
        bool found = false;
        for(int j = 0; j < A.size(); j++)
            if(A[j] == i) {
                found = true;
                break;
            }
        if(!found)
            return i;
    }
    return -1;
}

```

</details>

Time Complexity: $$O(n^2)$$​

Space Complexity: $$O(1)$$

### Using lookup table

<details>

<summary>Code</summary>

```cpp
int Solution::firstMissingPositive(vector<int> &A) {
    vector<bool> seen(A.size() + 1, false);

    for(int x: A)
        seen[x] = true;

    for(int i = 1; i < seen.size(); i++)
        if(!seen[i])
            return i;

    return -1;    
}
```

</details>

Time Complexity: $$O(n)$$

Space Complexity: $$O(n)$$

### Using Sorting

<details>

<summary>Code</summary>

```cpp
int Solution::firstMissingPositive(vector<int> &A) {
    sort(A.begin(), A.end());
    int expected = 1;
    for(int x: A)
        if(x > expected)
            return expected;
        else if(x == expected)
            expected++;

    return expected;
}
```

</details>

Time Complexity: $$O(n\log n)$$​

Space Complexity: $$O(1)$$

### Optimal Solution

<details>

<summary>Code</summary>

```cpp
int Solution::firstMissingPositive(vector<int> &A) {
    int n = A.size();
    for(int i = 0; i < n; i++) 
        if(A[i] > 0 && A[i] <= n) {
            int pos = A[i] - 1;
            if(A[pos] != A[i]) {
                swap(A[pos], A[i]);
                i--;
            }
        }
    
    for(int i = 0; i < n; i++)
        if(A[i] != i + 1) return (i + 1);

    return n + 1;
}
```

</details>

Time Complexity: $$O(n)$$​

Space Complexity: $$O(1)$$
