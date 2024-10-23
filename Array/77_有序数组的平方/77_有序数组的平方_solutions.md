```cpp
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        for(int i=0;i<nums.size();i++)
            nums[i]=nums[i]*nums[i];
        sort(nums.begin(),nums.end());
        return nums;
    }
};

//2min  time：98%
//很简单？ 看看题解有没有其他解法
```
