# Compare Version Numbers

{% embed url="https://www.interviewbit.com/problems/compare-version-numbers/" %}

### Using int for in-range numbers

```cpp
int getRevision(const string &A, int &i) {
    if(i >= A.size())
        return 0;
        
    int rev = 0;
    while(i < A.size() && A[i] != '.') {
        rev = rev * 10 + A[i] - '0';
        i++;
    }        
    return rev;
}

int Solution::compareVersion(string A, string B) {
    int i = 0, j = 0;
    
    // until both A and B are exhausted
    while(i < A.size() || j < B.size()) {
        int v1 = getRevision(A, i);
        int v2 = getRevision(B, j);
        
        if(v1 < v2) 
            return -1;
        if(v1 > v2)
            return 1;
            
        i++, j++;            
    }
    
    return 0;
}

```

### Using Strings for large numbers

```cpp
string getRevision(const string &A, int &i) {
    if(i >= A.size())
        return "0";
    
    string rev = "";
    
    while(i < A.size() && A[i] != '.') 
        rev += A[i++];
        
    return rev;
}

string removeLeadingZeros(string str) {
    int zeros = 0;
    while(zeros < str.size() && str[zeros] == '0')
        zeros++;
        
    return str.substr(zeros);
}

bool compare(string num1, string num2) {
    num1 = removeLeadingZeros(num1);
    num2 = removeLeadingZeros(num2);
    
    if(num1.size() == num2.size())
        return num1 < num2;
        
    return num1.size() < num2.size();
}


int Solution::compareVersion(string A, string B) {
    int i = 0, j = 0;
    
    while(i < A.size() || j < B.size()) {
        string v1 = getRevision(A, i);
        string v2 = getRevision(B, j);
        
        if(compare(v1, v2))
            return -1;
            
        if(compare(v2, v1))
            return 1;
            
            
        i++, j++;
    }
    
    return 0;   
}

```
