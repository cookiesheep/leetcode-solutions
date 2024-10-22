```cpp

// class Solution {
// public:
//     int removeElement(vector<int>& nums, int val) {
//         int k=nums.size();
//         for(int i=0;i<nums.size();i++)
//         {
//             if(nums[i]==val) 
//                 {
//                     k--;
//                     nums[i]=105;            //val最大为100
//                 }
//         }
        
//         sort(nums.begin(), nums.end());     //给vector排序时要用迭代器
//         return k;
//     }
// };


//15min
//完全自己写的 独立完成
//但是用的方法肯定不是很好（歪门邪道？） 再去看看题解
//我还发了一个题解   这是我力扣第一篇题解 记录一下！！！！

//正规方法：双指针法：

class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int i=0;       //慢指针
        for(int j=0;j<nums.size();j++)   //快指针
        {
            if(val!=nums[j])
            {
                nums[i]=nums[j];
                i++;
            }
        }
        return i;
    }
};

//这个是自己敲了一遍的双指针

```
