# Reorder Data in Log File

{% embed url="https://www.interviewbit.com/problems/reorder-data-in-log-files/" %}

<details>

<summary>Question</summary>

You are given an array of logs. Each log is a space-delimited string of words, where the first word is the identifier.\
\
There are two types of logs:

* Letter-logs: All words (except the identifier) consist of lowercase English letters.
* Digit-logs: All words (except the identifier) consist of digits.

Reorder these logs so that:

* The letter-logs come before all digit-logs.
* The letter-logs are sorted lexicographically by their contents. If their contents are the same, then sort them lexicographically by their identifiers.
* The digit-logs maintain their relative ordering.

Return the final order of the logs.

**Problem Constraints**\
1 <= logs.length <= 1000\
3 <= logs\[i].length <= 1000\
All the tokens of logs\[i] are separated by a single space.\
logs\[i] is guaranteed to have an identifier and at least one word after the identifier.\
\
\
**Input Format**\
The first argument is a string array A where each element is a log.\
\
**Output Format**\
Return the string array A after making the changes.\
\
**Example Input**\
Input 1:

```
A = ["dig1-8-1-5-1", "let1-art-can", "dig2-3-6", "let2-own-kit-dig", 
"let3-art-zero"]
```

Input 2:

```
A = ["a1-9-2-3-1","g1-act-car","zo4-4-7","ab1-off-key-dog","a8-act-zoo"]
```

**Example Output**\
Output 1:

```
["let1-art-can","let3-art-zero","let2-own-kit-dig","dig1-8-1-5-1",
"dig2-3-6"]
```

Output 2:

```
["g1-act-car", "a8-act-zoo", "ab1-off-key-dog", "a1-9-2-3-1", "zo4-4-7"]
```

**Example Explanation**\
Explanation 1:

```
The letter-log contents are all different, so their ordering is "art-can", "art-zero", "own-kit-dig".
The digit-logs have a relative order of "dig1-8-1-5-1", "dig2-3-6".
```

Explanation 2:

```
The array has been sorted restricted to the conditions given.
```

</details>

```cpp
inline string getType(string log) {
    return (isdigit(log.back())? "digit" : "letter");
}

inline string getMessage(string log) {
    return log.substr(log.find('-'));
}

inline string getID(string log) {
    return log.substr(0, log.find('-'));
}

bool comp(string log1, string log2) {
    // is log1 < log2?
    if(getMessage(log1) == getMessage(log2)) 
        return getID(log1) < getID(log2);
    return getMessage(log1) < getMessage(log2);
}
vector<string> Solution::reorderLogs(vector<string> &A) {
    vector<string> digits;

    // store digits in order
    for(string x: A) 
        if(getType(x) == "digit")
            digits.push_back(x);
    
    int digitCount = digits.size();
    int letterCount = A.size() - digitCount;

    // segregate
    int p1 = 0, p2 = A.size() - 1;
    while(p1 < p2) 
        if(getType(A[p1]) == "letter")
            p1++;
        else if(getType(A[p2]) == "digit")
            p2--;
        else 
            swap(A[p1++], A[p2--]);

    // place digit logs
    int k = 0;
    for(int i = letterCount; i < A.size(); i++)
        A[i] = digits[k++];

    // sort the letter logs
    sort(A.begin(), A.begin() + letterCount, comp);

    return A;
}
```

1. Store the digit logs in a separate vector to preserve their order.
2. Segregate the digits and letters such that letters appear before the digits.
3. Insert the digits back into the digits portion in order.&#x20;
4. Create a custom comparator function according to the specified condition.
5. Sort the letter part.
