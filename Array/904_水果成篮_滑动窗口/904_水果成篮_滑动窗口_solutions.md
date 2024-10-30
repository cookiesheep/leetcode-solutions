```cpp
class Solution {
public:
    int totalFruit(vector<int>& fruits) {
        int i=0,length,result=0,kind_num=0;
        vector<int> kind(100001, 0);
        for(int j=0;j<fruits.size();j++)
        {
            if(kind[fruits[j]]==0)
            {
                kind_num++;
            }    
            kind[fruits[j]]++;
            
            while(kind_num>2)
            {
                if(kind[fruits[i]]==1)
                    kind_num--;
                kind[fruits[i]]--;
                i++;
            }
            length=j-i+1;
            result=result<length?length:result;

        }
        return result;
    }
};

//58min  其实40min左右时就把大体代码敲好了   
//但是漏了一句代码  它的报错原因误解了我  调整了半天溢出问题
//本题没有完全独立完成  看了一部分思路以及题解  不过最终代码还是自己敲的
//有一个笔记我觉得一点要做：

// 最小滑窗模板：给定数组 nums，定义滑窗的左右边界 i, j，求满足某个条件的滑窗的最小长度。

// while j < len(nums):
//     判断[i, j]是否满足条件
//     while 满足条件：
//         不断更新结果(注意在while内更新！)
//         i += 1 （最大程度的压缩i，使得滑窗尽可能的小）
//     j += 1
// 最大滑窗模板：给定数组 nums，定义滑窗的左右边界 i, j，求满足某个条件的滑窗的最大长度。
// while j < len(nums):
//     判断[i, j]是否满足条件
//     while 不满足条件：
//         i += 1 （最保守的压缩i，一旦满足条件了就退出压缩i的过程，使得滑窗尽可能的大）
//     不断更新结果（注意在while外更新！）
//     j += 1


```
