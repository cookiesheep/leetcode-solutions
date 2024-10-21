### 别人的做题方法：数学法
这个方法很妙我觉得，以后可能会用到这个数学方法
1 4=1+3 9=1+3+5 16=1+3+5+7以此类推，模仿它可以使用一个while循环，不断减去一个从1开始不断增大的奇数，若最终减成了0，说明是完全平方数，否则，不是。

```cpp
class Solution 
{
public:
    bool isPerfectSquare(int num) 
    {
        int num1 = 1;
        while(num > 0) 
        {
            num -= num1;
            num1 += 2;
        }
        return num == 0;
    }
};

//原理:(n+1)^2-n^2=2n+1
```
作者：I3old MorseHDn
链接：https://leetcode.cn/problems/valid-perfect-square/solutions/93200/zhi-xing-yong-shi-0-ms-zai-suo-you-c-ti-jiao-zh-44/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
