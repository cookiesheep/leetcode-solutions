# 349. 两个数组的交集

### 简单
### 相关标签  数组  哈希表  双指针  二分查找  排序
相关企业
给定两个数组 nums1 和 nums2 ，返回 它们的 
交集
 。输出结果中的每个元素一定是 唯一 的。我们可以 不考虑输出结果的顺序 。

 
```
示例 1：

输入：nums1 = [1,2,2,1], nums2 = [2,2]
输出：[2]
示例 2：

输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出：[9,4]
解释：[4,9] 也是可通过的
 ```

提示：

1 <= nums1.length, nums2.length <= 1000
0 <= nums1[i], nums2[i] <= 1000

# solutions
```cpp
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> ans;
        unordered_set<int> set;
        for(int i=0;i<nums1.size();i++)
            set.insert(nums1[i]);
        for(int i=0;i<nums2.size();i++)
        {
            if(set.find(nums2[i])!=set.end())
                ans.insert(nums2[i]);
        }
        return vector<int>(ans.begin(),ans.end());
    }
};
//8min
//这题也简单  不重复无顺序非常体现了unordered_set的妙处
//但是有一个要注意 的点：return的时候要返回vector
//vector<int>(ans.begin(), ans.end())：
//使用集合 ans 的迭代器范围，创建一个包含相同元素的新 std::vector<int> 对象。
```
