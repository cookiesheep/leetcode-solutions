```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int i=0;
        for(int j=0;j<nums.size();j++)
        {
            if(nums[j]!=0)
            {
                nums[i]=nums[j];
                i++;
            }
        }
        for(int k=nums.size()-1;k>=i;k--)   //这个特殊一点 要检查所有
            nums[k]=0;                  //上面的操作仅是覆盖 意味着是有0都没有了
        return ;
    }
};

//6min    time:100%
//独立完成！
```
