# ⭐ Integer to Roman

{% embed url="https://www.interviewbit.com/problems/integer-to-roman/" %}

```cpp
string Solution::intToRoman(int A) {
        vector<pair<string, int>> symbols = {
        make_pair("M", 1000),
        make_pair("CM", 900),
        make_pair("D", 500),
        make_pair("CD", 400),
        make_pair("C", 100),
        make_pair("XC", 90),
        make_pair("L", 50),
        make_pair("XL", 40),
        make_pair("X", 10),
        make_pair("IX", 9),
        make_pair("V", 5),
        make_pair("IV", 4),
        make_pair("I", 1)
    };
    
    string res = "";
    
    for(auto p: symbols) 
        if(A >= p.second) {
            int count = A / p.second;
            for(int i = 1; i <= count; i++)
                res += p.first;        
            A %= p.second;
        }
        
    return res;
}

```
