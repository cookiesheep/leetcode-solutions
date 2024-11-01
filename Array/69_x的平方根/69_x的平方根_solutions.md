```cpp
// class Solution {
// public:
//     int mySqrt(int x) {
//     //先找一个有序数组吧  我想的是：1,2,3,...,x
//     //然后在这个数组中找到第一个平方大于x的数 但这样就不是二分了 先试试吧  
//     //感觉时间会超  x的值太大了    
//     for(int i=0;i<=x;i++)
//         if(i*i==x) return i; 
//         else if(i*i>x) return i-1;
//     return -1;
//     }
// };
// //果然时间超了  这个方法不行  诶好像是内存超了



class Solution {
public:
    int mySqrt(int x) {
    int left=0,right=x,ans=0;
    while(left<=right)
    {
        long long int mid=left+(right-left)/2;
        if(mid*mid>x) right=mid-1;
        else if(mid*mid<=x) 
        {
            ans=mid;
            left=mid+1;
        }        
    }
    return ans;
    }
};

//45min 
// 二分写了一个非常接近的，但是还是细节没完成 最后return什么懵掉了
// 最终还是看的题解  希望下次能够完完全全得独立完成
```

#### 解释：
### 示例：x = 27

初始值：

- `l = 0`（左边界）
- `r = 27`（右边界）
- `ans = -1`（存储结果）

### 第一次循环
计算 `mid = l + (r - l) / 2 = 0 + (27 - 0) / 2 = 13`。  
判断 `(long long)mid * mid <= x`，即 `13 * 13 = 169`，大于 `27`，所以：
- 更新 `r = mid - 1 = 13 - 1 = 12`。
- `ans` 没有更新，因为 `13^2 > 27`。

### 第二次循环
计算 `mid = 0 + (12 - 0) / 2 = 6`。  
判断 `6 * 6 = 36`，大于 `27`，所以：
- 更新 `r = mid - 1 = 6 - 1 = 5`。
- `ans` 依然没有更新，因为 `6^2 > 27`。

### 第三次循环
计算 `mid = 0 + (5 - 0) / 2 = 2`。  
判断 `2 * 2 = 4`，小于 `27`，所以：
- 更新 `ans = mid = 2`（当前找到的平方根的候选值）。
- 更新 `l = mid + 1 = 2 + 1 = 3`，进入右半部分查找。

### 第四次循环
计算 `mid = 3 + (5 - 3) / 2 = 4`。  
判断 `4 * 4 = 16`，小于 `27`，所以：
- 更新 `ans = mid = 4`（当前找到的平方根的候选值）。
- 更新 `l = mid + 1 = 4 + 1 = 5`，进入右半部分查找。

### 第五次循环
计算 `mid = 5 + (5 - 5) / 2 = 5`。  
判断 `5 * 5 = 25`，小于 `27`，所以：
- 更新 `ans = mid = 5`（当前找到的平方根的候选值）。
- 更新 `l = mid + 1 = 5 + 1 = 6`。

此时，`l > r`（`6 > 5`），循环结束，返回 `ans = 5`。

---

### 动态过程总结：
- 初始范围是 `[0, 27]`。
- 第一次计算 `mid = 13`，平方大于 `27`，缩小右边界。
- 第二次计算 `mid = 6`，平方大于 `27`，继续缩小右边界。
- 第三次计算 `mid = 2`，平方小于 `27`，更新答案，扩大左边界。
- 第四次计算 `mid = 4`，平方小于 `27`，更新答案，继续扩大左边界。
- 第五次计算 `mid = 5`，平方小于 `27`，更新答案，直到 `l > r` 时结束。

最终得到 `5`，即 `27` 的平方根的整数部分。

---

### 解释：
在这个过程中，我们通过每次计算中间值 `mid` 来缩小查找范围，逐步接近目标结果。在每个步骤中，要么更新 `ans`（表示当前的候选解），要么缩小左右边界。最终找到的答案是 `5`，因为 `5^2 = 25`，而 `6^2 = 36` 大于 `27`，所以平方根的整数部分是 `5`。

这个示例展示了如何通过多次迭代和二分查找的方法高效地处理较大的数字。

