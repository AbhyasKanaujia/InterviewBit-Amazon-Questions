# Largest Number

{% embed url="https://www.interviewbit.com/problems/largest-number/" %}
Given a list of non negative integers, arrange them such that they form the largest number.
{% endembed %}

1. Sort the input such that simply appending them one after another forms the result
2. Sort using special comparator function that checks for both possibilities of positions for any two given numbers.

```cpp
bool comp(string n1, string n2) {
    return n1 + n2 > n2 + n1;
}

string Solution::largestNumber(const vector<int> &A) {
    string result;
    vector<string> str;
    bool allZero = true;
    for(int x: A) {
        if(allZero && x) allZero = false;
        str.push_back(to_string(x));
    }

    if(allZero) return "0";

    sort(str.begin(), str.end(), comp);
    for(string x: str)
        result += x;

    return result;
}

```
