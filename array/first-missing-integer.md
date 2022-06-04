# First Missing Integer

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

Time Complexity: $$O(n\log n)$$​

Space Complexity: $$O(1)$$​
