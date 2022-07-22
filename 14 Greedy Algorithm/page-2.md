# ⭐ Majority Element

## Using Map

```cpp
int Solution::majorityElement(const vector<int> &A) {
    map<int, int> freq;
    for(int x: A)
        freq[x]++;
        
    int maxElement = -1;
    int maxFreq = 0;
    
    for(pair<int,int> elementFreq : freq) 
        if(elementFreq.second > maxFreq) {
            maxFreq = elementFreq.second;
            maxElement = elementFreq.first;
        }
        
    return maxElement;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(n)$$​

## Voting Technique

```cpp
int Solution::majorityElement(const vector<int> &A) {
    int hero = -1;
    int freqHero = 0;
    for(int x: A) {
        if(freqHero == 0)
            hero = x;
            
        if(hero != x)
            freqHero--;
        else
            freqHero++;
    }
    
    return hero;
}
```

Time Complexity: $$O(n)$$​

Space Complexity: $$O(1)$$​
