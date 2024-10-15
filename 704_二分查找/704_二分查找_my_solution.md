```cpp
#include<stdio.h>
#include<iostream>
#include<string>
#include<cctype>
#include <vector>


//第一种解法：暴力
// class Solution {
// public:
//     int search(vector<int>& nums, int target) {
//         bool flag=true;
//         int ans;
//         for(int i=0;i<nums.size();i++)
//         {
//             if(nums[i]==target)
//             {
//                 ans=i;
//                 flag=false;
//                 break;
//             }
//         }
//         if(flag) ans= -1;
//         return ans;
//     }
    
// };



// // int main()
// // {
// //     vector<int> nums;
// //     char a;
// //     cin>>a;
// //     while(a!=']')
// //     {   string s="";
// //         while(a!=',')
// //         {
// //             cin>>a;
// //             s+=a;
// //         }
// //         nums.push_back(stoi(s));
// //     }
// //     for (size_t i = 0; i < nums.size(); ++i) {
// //     std::cout << nums[i] << " ";}

// //     return 0;
// // }

//一下是一些总结：
// 这是我第一次做力扣，本题花时间38min，其实本来函数部分是一下子就写好了
// 但是不知道力扣会主动生成main函数，傻乎乎得写了半天main函数，我感觉main函数里处理输入还是挺难的。
// 然后我第一次做题没有用二分，用时击败26%，空间击败73%，我现在再去看题解优化一下。


// 第二次写代码：二分查找（我以前敲过的）

class Solution{
    public:
    int search(vector<int>& nums,int target)
    {
        int left=0,right=nums.size()-1;
        while(left<=right)
        {
            int mid=left+(right-left)/2;
            int num=nums[mid];
            if(num==target)
            {
                return mid;
            }
            else if(num>target)
            {
                right=mid-1;
            }
            else left=mid+1;
        }
        return -1;
    }
};
```
