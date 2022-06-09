# ⭐ Capacity To Ship Packages Within B Days

{% embed url="https://www.interviewbit.com/problems/capacity-to-ship-packages-within-b-days/" %}

```cpp
bool check(const vector<int> &arr, int days, int capacity) {
    int daysRequired = 1;
    int shipment = 0;
    for(const int &x: arr) {
        shipment += x;
        if(shipment > capacity) {
            shipment = x;
            daysRequired++;
        }
    }

    return daysRequired <= days;
}

int Solution::solve(vector<int> &A, int B) {
    int low = *max_element(A.begin(), A.end());
    int high = 1e9;

    while(low < high) {
        int mid = low + ((high - low) >> 1);
        if(check(A, B, mid))
            high = mid;
        else
            low = mid + 1;
    }
    return high;
}

```
