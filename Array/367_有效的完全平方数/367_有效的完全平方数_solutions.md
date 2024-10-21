```cpp
class Solution {
public:
    bool isPerfectSquare(int num) {
        int left=0,right=num;
        bool flag=1;
        while(left<=right)
        {
            long long int mid=left+(right-left)/2;
            if(mid*mid<num) left=mid+1;
            else if(mid*mid>num) right=mid-1;
            else { flag=0; return 1;}
        }
        if(flag) return 0;
        return -1;
    }
};

//7,8min就做出来啦
//这是我第一道没看题解 且写出来时间空间还不错的题  有点小成就感 记录一下
```
