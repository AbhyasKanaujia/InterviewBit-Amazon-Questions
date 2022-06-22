# ⭐ k-th Permutation

{% embed url="https://www.interviewbit.com/problems/k-th-permutation/" %}

{% embed url="https://www.youtube.com/watch?v=wT7gcXLYoao" %}

```cpp
vector<int> Solution::findPerm(int n, long k) {
    int fact = 1;
    vector<int> numbers;
    for(int i = 1; i < n; i++) {
        fact = fact * i;
        numbers.push_back(i);
    }
    numbers.push_back(n);

    vector<int> res;

    k = k - 1;

    while(true) {
        res.push_back(numbers[k / fact]);
        numbers.erase(numbers.begin() + k / fact);
        if(numbers.size() == 0)
            break;
        k = k % fact;
        fact = fact / numbers.size();
    }
    return res;
}

```
