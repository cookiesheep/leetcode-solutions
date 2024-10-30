```cpp
//法一：暴力  会超时

// class Solution {
// public:
//     int minSubArrayLen(int target, vector<int>& nums) {
//         int min_length=INT32_MAX;    //有一个写法：int min_length = INT32_MAX;
//         int sum=0;
//         for(int i=0;i<nums.size();i++)
//         {
//             sum=0;
//             for(int j=i;j<nums.size();j++)
//             {
//                 int length;
//                 sum+=nums[j];
//                 if(sum>=target) 
//                 {
//                     length=j-i+1;
//                     if(min_length>length) min_length=length;
//                     break;
//                 }
                
//             }
//         }
//          // 如果min_length没有被赋值的话，就返回0，说明没有符合条件的子序列
//         return min_length == INT32_MAX ? 0 : min_length;
//     }
// };


//法二：滑动窗口


class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int i=0,sum=0;
        int length,result=INT32_MAX;
        for(int j=0;j<nums.size();j++)
        {
            sum+=nums[j];
            while(sum>=target)
            {
                length=j-i+1;
                result=result<length?result:length;
                sum-=nums[i];
                i++;
            }
        }
        return result==INT32_MAX?0:result;
    }
};


//昨天感觉好难没做  今天大概10min就写出来了
//虽然看了滑动窗口的原理  但代码主要还是自己实现的，不要畏难
//启发：算法真的很妙  如果没有提前看过动画真的不理解想不到还可以这么解决问题
//我现在主要的做法应该是多学习前人的算法  站在他们的肩膀上   以后看看能不能提出我自己的算法
```
