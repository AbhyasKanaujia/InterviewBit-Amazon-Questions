# Ugly Number II

{% embed url="https://leetcode.com/problems/ugly-number-ii/" %}

```cpp
class Solution {
public:
    int nthUglyNumber(int n) {
        // we solve this question not by gettting all the numbers 1, 2, 3... 
        // and checking if each number is ugly or not. 
        // Instead we solve it by generating only the useful numbers.
        
        // usefull numbers are built by multiples of 2, 3, 5
        // then these numbers can be stored in sorted order
        // until n such numbers have been stored
        
        vector<int> uglyNumbers(n);
        uglyNumbers[0] = 1;
        
        int i2, i3, i5;
        i2 = i3 = i5 = 0;
        
        for(int index = 1; index < n; index++) {
            int choiceByUsing2 = 2 * uglyNumbers[i2];
            int choiceByUsing3 = 3 * uglyNumbers[i3];
            int choiceByUsing5 = 5 * uglyNumbers[i5];
            
            int choice = min(choiceByUsing2, min(choiceByUsing3, choiceByUsing5));
            
            uglyNumbers[index] = choice;
            
            if(uglyNumbers[index] == choiceByUsing2) 
                i2++;
            
            if(uglyNumbers[index] == choiceByUsing3)
                i3++;
            
            if(uglyNumbers[index] == choiceByUsing5)
                i5++;
            
        } 
        
        return uglyNumbers[n - 1];
    }
};
```
