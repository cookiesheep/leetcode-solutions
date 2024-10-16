二分法第一种写法
以这道题目来举例，以下的代码中定义 target 是在一个在左闭右闭的区间里，也就是[left, right] （这个很重要）。

这就决定了这个二分法的代码如何去写，大家看如下代码：

大家要仔细看注释，思考为什么要写while(left <= right)， 为什么要写right = middle - 1。
```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int n = nums.size();
        int left = 0;
        int right = n - 1; // 定义target在左闭右闭的区间里，[left, right]
        while (left <= right) { // 当left==right，区间[left, right]依然有效
            int middle = left + ((right - left) / 2);// 防止溢出 等同于(left + right)/2
            if (nums[middle] > target) {
                right = middle - 1; // target 在左区间，所以[left, middle - 1]
            } else if (nums[middle] < target) {
                left = middle + 1; // target 在右区间，所以[middle + 1, right]
            } else { // nums[middle] == target
                return middle;
            }
        }
        // 分别处理如下四种情况
        // 目标值在数组所有元素之前  [0, -1]
        // 目标值等于数组中某一个元素  return middle;
        // 目标值插入数组中的位置 [left, right]，return  right + 1
        // 目标值在数组所有元素之后的情况 [left, right]， 因为是右闭区间，所以 return right + 1
        return right + 1;
    }
};
```
时间复杂度：O(log n)
空间复杂度：O(1)
效率如下： 35_搜索插入位置2

#二分法第二种写法
如果说定义 target 是在一个在左闭右开的区间里，也就是[left, right) 。

那么二分法的边界处理方式则截然不同。

不变量是[left, right)的区间，如下代码可以看出是如何在循环中坚持不变量的。

大家要仔细看注释，思考为什么要写while (left < right)， 为什么要写right = middle。
```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int n = nums.size();
        int left = 0;
        int right = n; // 定义target在左闭右开的区间里，[left, right)  target
        while (left < right) { // 因为left == right的时候，在[left, right)是无效的空间
            int middle = left + ((right - left) >> 1);
            if (nums[middle] > target) {
                right = middle; // target 在左区间，在[left, middle)中
            } else if (nums[middle] < target) {
                left = middle + 1; // target 在右区间，在 [middle+1, right)中
            } else { // nums[middle] == target
                return middle; // 数组中找到目标值的情况，直接返回下标
            }
        }
        // 分别处理如下四种情况
        // 目标值在数组所有元素之前 [0,0)
        // 目标值等于数组中某一个元素 return middle
        // 目标值插入数组中的位置 [left, right) ，return right 即可
        // 目标值在数组所有元素之后的情况 [left, right)，因为是右开区间，所以 return right
        return right;
    }
};
```
时间复杂度：O(log n)
空间复杂度：O(1)
#总结
希望通过这道题目，大家会发现平时写二分法，为什么总写不好，就是因为对区间定义不清楚。

确定要查找的区间到底是左闭右开[left, right)，还是左闭又闭[left, right]，这就是不变量。

然后在二分查找的循环中，坚持循环不变量的原则，很多细节问题，自然会知道如何处理了。
