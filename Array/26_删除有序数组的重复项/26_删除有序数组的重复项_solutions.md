```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int k=1;
        for(int i=1;i<nums.size();i++)
        {
            if(nums[i]!=nums[i-1])
            {
                nums[k]=nums[i];
                k++;
            }
        }
        return k;
    }
};

//34min  时间100%
//还借鉴了一下gpt
//其实和上一题27几乎一模一样 但是有个地方变了一下我没反应过来
```
