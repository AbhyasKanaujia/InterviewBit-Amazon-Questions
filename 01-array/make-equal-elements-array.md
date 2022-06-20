# Make equal elements Array

{% embed url="https://www.interviewbit.com/problems/make-equal-elements-array/" %}

```cpp
int Solution::solve(vector<int> &A, int B) {;
    int avg = 0;
    set<int> unique(A.begin(), A.end());
    
    for(const int &x: unique)
        avg += x;

    avg /= unique.size();

    for(int x: unique)
        if(x == avg || x + B == avg || x - B == avg)
            continue;
        else
            return false;

    return true;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(n)$$​

```
x = 1
For arr = 5 6 4 4 6
arr + x = 6 7 5 5 7
arr - x = 4 5 3 3 5
```

Each column represents: no change, add `x` and subtract `x` in order for the top to bottom

Observe that 5 is present in each column

That is to say, 5 can be formed by either adding or subtracting or by doing nothing

Also notice that 5 is the average of the whole array

Thus we need to find the average and check if: each digit is already equal to the average or if it can be made equal to the average by adding or subtracting `x`
