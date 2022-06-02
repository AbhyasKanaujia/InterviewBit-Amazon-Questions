# ❌ Find Duplicate in Array

{% embed url="https://www.interviewbit.com/problems/find-duplicate-in-array/" %}

### Last attempt

Use N / 2 array and each index represent 2 value

```cpp
int Solution::repeatedNumber(const vector<int> &A) {
    vector<int> counter(A.size() / 2);

    for(const int &x: A)
        counter[(x - 1) / 2]++;

    int repeating = -1;
    for(int i = 0; i < counter.size(); i++)
        if(counter[i] > 1) {
            repeating = i; 
            break;
        }

    int a = 0, b = 0;

    for(const int &x: A) 
        if(x == 2 * repeating + 1)
            a++;
        else if(x == 2 * repeating + 2)
            b++;


    if(a > b)
        return 2 * repeating + 1;
    else   
        return 2 * repeating * 2;

}
```
