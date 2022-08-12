# ⭐ Rotated Sorted Array Search

{% embed url="https://www.interviewbit.com/problems/rotated-sorted-array-search/" %}

```cpp
class Solution {
private:
    int getPivot(vector<int> &nums) {
        // if first <= last then not rotated
        // 1st element is pivot
        if(nums.front() <= nums.back())
            return 0;
    
        int low = 0, high = nums.size() - 1;
        int pivot = -1;
    
        // until low crosses high
        while(low <= high) {
            int mid = low + ((high - low) >> 1);
            
            // if mid >= first => on first line
            // skip this mid rightward
            if(nums[mid] >= nums[0])
                low = mid + 1;
            // if mid < first => on second line
            // could be the solution. 
            // store and skip mid leftward
            else {
                pivot = mid;
                high = mid - 1;
            }
        }
        
        return pivot;
    }
    
    int binarySearch(vector<int> &nums, int low, int high, int target) { 
        while(low <= high) {
            int mid = low + ((high - low) >> 1);
            
            if(nums[mid] == target)
                return mid;
            else if(nums[mid] > target)
                high = mid - 1;
            else 
                low = mid + 1;
        }
        
        return -1;
    }
    
public:
    int search(vector<int>& nums, int target) {
        int pivot = getPivot(nums);
        
        // if target < nums[0] => the element is on the second line
        // if pivot == 0 => the array is in ascending order
        // in both cases search pivot to size - 1
        if(target < nums[0] || pivot == 0)
            return binarySearch(nums, pivot, nums.size() - 1, target);
        // if target >= nums[0] => the element is on the first line
        // sarch from begin to pivot - 1
        else
            return binarySearch(nums, 0, pivot - 1, target);
    }
};
```

