```cpp
// class Solution {
// public:
//     vector<int> searchRange(vector<int>& nums, int target) {
//         int left=0,right=nums.size()-1;
//         vector<int> index;
//         int len=0;
//         while(left<=right)
//         {
//             int mid=left+(right-left)/2;
//             int num=nums[mid];
//             if(num<target) left=mid+1;
//             else if(num>target) right=mid-1;
//             else index.push_back(mid);      //重大逻辑问题！！！
//         }        //我原本的思路是不停地找，一找到一个target就把它的下标存入数组
//                  //但是，我忘了，一旦找到target后左右边界都不更新了，死循环！！
//         vector<int> ans;
//         sort(index.begin(),index.end());
//         if(index.empty()) ans={-1,-1};
//         else ans={index[0],index[index.size()-1]};
//         return ans;
//     }
// };
//45min 做了一个错的
//下面是从gpt那获得的思路，分别找左边界和右边界，用两个二分！非常妙！


class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        vector<int> ans={-1,-1};
    //第一个二分找左边界
        int left=0,right=nums.size()-1;
        while(left<=right)
        {
            int mid=left+(right-left)/2;
            int num=nums[mid];
            if(num<target) left=mid+1;
            else right=mid-1;  //关键代码***，我觉得我对二分的过程还是欠一些理解
        }
        // 检查左边界是否存在
        if (left >= nums.size() || nums[left] != target) {
            return ans; // 没有找到目标，返回 {-1, -1}
        }
        ans[0] = left;  // 记录左边界
        //重置右边界
        right=nums.size()-1;
        while(left<=right)
        {
            int mid=left+(right-left)/2;
            int num=nums[mid];
            if(num>target) right=mid-1;
            else left=mid+1;  
        }
        ans[1] = right;  // 记录右边界
    return ans;
    }
};
```
