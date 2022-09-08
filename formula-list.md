# 🧪 Formula List

## Basic <a href="#prevent-iterator-from-moving-forward-in-for-loop." id="prevent-iterator-from-moving-forward-in-for-loop."></a>

### Prevent iterator from moving forward in `for` loop. <a href="#prevent-iterator-from-moving-forward-in-for-loop." id="prevent-iterator-from-moving-forward-in-for-loop."></a>

```cpp
char ch;

for(int i = 1; i <= 10; i++) {
    cout << "Iteration " << i << endl;
    cout << "repeat iteration (y/n): ";
    cin >> ch;
    
    if(ch == 'y')
    i--;
}
```

Sometimes you might want to work with the same value of the iterator. Example: See solution for [First Missing Integer](https://www.interviewbit.com/problems/first-missing-integer/)

## Array

* Address of index `i` = `base address` + `index` \* `size` of each element
* When working with a group of people in a circular arrangement(or any similar situation), think of how a `queue` might be used here.&#x20;

## Binary Search

### Getting Mid while Avoids Integer Overflow

$$
mid=low+((high-low)>>1)
$$

:bomb: `mid = low + (high - low) >> 1` will not work. >>'s precedence is lower, so it needs to be in parentheses.

## Math

| Problem        | Approach              |
| -------------- | --------------------- |
| Primality Test | Sieve of Eratosthenes |

### GCD Euclid's Formula

See Main Article

$$
\text{GCD}(a, b) = \left\{ \begin{array}{ll} b & \text{when } a = 0 \\ a & \text{when } b = 0 \\ GCD(a \% b, b) & \text{when } a > b \\ GCD(a, b \% a) & \text{when } b > a \\ \end{array} \right.
$$

### Fast Exponentiation

See Main Article

$$
x^n=\left\{ \begin{array}{ll} x^\frac{n}{2}\times x^\frac{n}{2}&\text{when x is even and } n >= 0 \\ x^\frac{n}{2}\times x^\frac{n}{2} \times x&\text{when x is odd and } n >= 0 \\ x^\frac{n}{2}\times x^\frac{n}{2}&\text{when x is even and } n < 0 \\ x^\frac{n}{2}\times x^\frac{n}{2} \times \frac{1}{x} &\text{when x is odd and } n < 0 \\ \end{array} \right.
$$

### Compare Numbers Represented as String

```cpp
bool compare(string s1, string s2) { // is s1 smaller than s2
    if(s1.length() == s2.length()) 
        return s1 < s2;
    return s1.length() < s2.length();
}
```

Useful when comparing extremely large numbers that cannot otherwise be stored in any other data type

### Removing Leading 0s from a Number in String

```cpp
string removeLeadingZeros(string str) {
    int zeros = 0;
    while(zeros < str.size() && str[zeros] == '0')
        zeros++;
        
    return str.substr(zeros);
}
```

### Compare double type numbers

```cpp
if(abs(a - b) < 1e-9)
	cout << "Same";
else
	cout << "Not Same";
```

Two double-type numbers could be the same but could evaluate as false due to precision error when compared using `==` for equality.

Another way to say that two double numbers are equal is to say that the distance between them is less than $$\epsilon$$​, where $$\epsilon$$ is a very small number.​

### Check whether a double type contains Integer

```cpp
inline bool isInteger(const double &x) {
    return (x - (int)x != 0);
}
```

If a number is not an integer, for example, 5.5, then its difference with its integer part will be non-zero.

If it is an integer, then the difference is 0.

$$
5.5-5=0.5 \ne 0\\ 5.0-5=0
$$

### $$^nC_r$$

```cpp
int nCr(int n, int r) {
    if(n == 0 || r == 0 || n == r)
        return 1;

    r = min(r, n - r);

    int res = 1;
    for(int i = 1; i <= r; i++) 
        res = res * (n - i + 1) / i;
    
    return res;
}
```

Time Complexity: $$O(min(r, n - r))$$

### Property of nCr

$$
^nC_r=^{n-1}C_r+^{n-1}C_{r-1}
$$

```cpp
int getnCr(int n, int r, vector<vector<int>> &savedResult) {
    r = min(r, n - r);
    
    if(r == 0)
        return 1;
        
    if(r == 1)
        return n;
        
    if(savedResult[n][r])
        return savedResult[n][r];
        
    return savedResult[n][r] = 
            (getnCr(n - 1, r, savedResult) + getnCr(n - 1, r - 1, savedResult));
}
```

### $$^nP_r$$

### Property of nPr

$$
^nP_r=^{n-1}P_{r}+r \times ^{n-1}P_{r-1}
$$

```cpp
int P(int n, int r) {
    long long nPr[n + 1][r + 1];
    
    for(int i = 1; i <= r; i++)
        nPr[0][i] = 0;
    
    for(int i = 0; i <= n; i++)
        nPr[i][0] = 1;
    
    for(int i = 1; i <= n; i++)
        for(int j = 1; j <= r; j++)
            nPr[i][j] = (nPr[i - 1][j] + (j * nPr[i - 1][j - 1])) % 1000000007;
    
    return nPr[n][r];
}
```

### Power of two

```cpp
(n & (n - 1) == 0) ? "Yes" : "No";
```

## Bit Manipulation

### Check if bit is set

```cpp
bool isSet(int num, int posFromRight) {
    return num & (1 << (posFromRight - 1));
}
```

### Set a bit

```cpp
int set(int num, int posFromRight) {
    return num | (1 << (posFromRight - 1));
}
```

### Multiply by 2^k

$$num \times 2^k$$

```cpp
int multiply(int num, int k) {
    return num << k; // num * 2 ^ k
}
```

### Check if a number is odd or even

```cpp
bool isEven(int num) {
    return (num & 1) ? true : false;
}
```

## String

| Problem         | Approach                                                                                                                    |
| --------------- | --------------------------------------------------------------------------------------------------------------------------- |
| Palindrome Test | Two Pointer Approach                                                                                                        |
| Anagram Test    | <ul><li>Count of each character in both the strings will be same.</li><li>Use <code>map</code> or a lookup table.</li></ul> |



## Linked List

### Edge Cases

| Case                                  | Problem                                 | Handling                            |
| ------------------------------------- | --------------------------------------- | ----------------------------------- |
| Linked List has single or no elements | Accessing `ptr -> next` throws an error | `if(!A \|\| !(A -> next)) reutrn A` |

### Get Length of a Linked List

```cpp
int getLength(ListNode* A) {
    int count = 0;
    while(A) {
        count++;
        A = A -> next;
    }
    return count;
}
```

### Get nth Node from Front

Here $$n\in [1, A.length]$$​

```cpp
ListNode *getNode(ListNode *A, int n) {
    while(--n) 
        A = A -> next;
    
    return A;
}
```

### Get the Last Node of a Linked List

```cpp
ListNode* getEnd(ListNode *ll) {
    if(!ll) return ll;
    
    while(ll -> next)
        ll = ll -> next;
        
    return ll;
}
```

### Reverse a Linked List

```cpp
ListNode *reverseLL(ListNode *ll) {
    ListNode *prev = NULL;
    ListNode *current = ll;
    
    while(current) {
        ListNode *next = current -> next;
        current -> next = prev;
        prev = current;
        current = next;
    }
    
    return prev;
}
```

### Get the Middle Element of a Linked List

<pre class="language-cpp"><code class="lang-cpp"><strong>ListNode *getMiddle(ListNode *A) {
</strong>    ListNode *slow = A, *fast = A;
    while(fast &#x26;&#x26; fast -> next &#x26;&#x26; fast->next->next) {
        slow = slow -> next;
        fast = fast -> next -> next;
    }
    return slow;
}</code></pre>

```bash
Odd length: 
    1 2 3 4 5 6 7
          ^
Even Length: 
    1 2 3 4 5 6 7 8
          ^
```

#### To get 5 as the middle element in event elements

Initialize `fast` with `head->next`

```cpp
ListNode *getMiddle(ListNode *A) {
    ListNode *slow = A, *fast = next;
    while(fast && fast -> next) {
        slow = slow -> next;
        fast = fast -> next -> next;
    }
    return slow;
}
```

```
Odd length: 
    1 2 3 4 5 6 7
          ^
Even Length: 
    1 2 3 4 5 6 7 8
            ^* special, comapre to previous code
```

## Binary Tree

### Iterative Traversal Algorithm

#### Inorder Traversal

```cpp
vector<int> inOrder(Node* root) {
    vector<int> res;
    stack<Node *> s;
    Node* current = root;
    
    while(current || !s.empty()) {
        while(current) {
            s.push(current);
            current = current->left;
        }
        
        current = s.top();
        s.pop();
        
        res.push_back(current->data);
        current = current->right;
    }
    
    return res;
}
```
