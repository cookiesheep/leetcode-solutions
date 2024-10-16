```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int left=0,right=nums.size()-1;
        // int ans;
        while(left<=right)
        {
            int mid=left+(right-left)/2;
            int num=nums[mid];
            // ans=mid;
            if(num>target) right=mid-1;
            else if(num<target) left=mid+1;
            else  return mid; 

        }
        // 如果没找到，返回的是插入位置，即 left!!???
        return left;  //*
    }
};

//用时：22min
//难点：如果目标值不存在于数组中，返回它将会被按顺序插入的位置。
//    这个的处理方法我觉得我主要是通过找规律看出来它就是加上一
//    但是逻辑上可能不是特别明白  我开始的处理方法是return mid+1
//                              测试用例对了但没通过
//    后来问了一下gpt，它说直接return left   我还没有特别想明白为什么
//    原因：二分查找结束后：
//          left 最终指向第一个大于或等于 target 的位置，也就是目标值的插入位置。
```
