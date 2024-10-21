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
