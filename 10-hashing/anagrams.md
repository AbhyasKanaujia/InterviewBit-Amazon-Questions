# ⭐ Anagrams

{% embed url="https://www.interviewbit.com/problems/anagrams/" %}

## Using Frequency Map

### Only for +ve Numbers

{% embed url="https://www.youtube.com/watch?v=NNBQik4phMI" %}

<details>

<summary>What is a Frequency Map?</summary>

![](<../.gitbook/assets/image (2).png>)

</details>

{% tabs %}
{% tab title="C++" %}
```cpp
vector<vector<int> > Solution::anagrams(const vector<string> &A) {
    map<map<char,int>, vector<int>> frequencyMapToIndex;
    
    for(int i = 0; i < A.size(); i++) {
        map<char, int> freqMap;
        for(const char &ch: A[i]) 
            freqMap[ch]++;
            
        frequencyMapToIndex[freqMap].push_back(i + 1);
    }
    
    vector<vector<int>> res;
    for(auto group: frequencyMapToIndex)
        res.push_back(group.second);
        
    return res;
}
```

Not Accepted
{% endtab %}
{% endtabs %}
