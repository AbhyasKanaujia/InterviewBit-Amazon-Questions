# Majority Element

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
