---
cover: >-
  https://images.unsplash.com/photo-1536689679813-466c89d34c7e?crop=entropy&cs=tinysrgb&fm=jpg&ixid=MnwxOTcwMjR8MHwxfHNlYXJjaHw2fHxmbGlwfGVufDB8fHx8MTY1NDUyODgzMw&ixlib=rb-1.2.1&q=80
coverY: 127.426597582038
---

# Flip

{% embed url="https://www.interviewbit.com/problems/flip/hints/" %}
One operation means changing character **0** to **1** and vice-versa.\
our aim is to perform **ATMOST** one operation such that in the final string number of **1s** is maximised.
{% endembed %}

```cpp
vector<int> Solution::flip(string A) {
    int n = A.size();

    vector<int> res;
    vector<int> kaden;

    int hasZero = false;
    for(int x: A) 
        if(x == '0') {
            hasZero = true;
            kaden.push_back(1);
        } else 
            kaden.push_back(-1);

    if(!hasZero)
        return res;

    res.push_back(0);
    res.push_back(0);

    int sum = -1, maxSum = -1;
    int left = 0;

    for(int i = 0; i < n; i++) {
        if(sum < 0) {
            left = i + 1;
            sum = kaden[i];   
        } else 
            sum += kaden[i];

        if(sum > maxSum) {
            maxSum = sum;
            res[0] = left;
            res[1] = i + 1; 
        }
    }

    return res;
}

```

{% embed url="https://www.youtube.com/watch?v=Etkf8sRQdbU" %}
