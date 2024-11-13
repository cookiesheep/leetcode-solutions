```cpp
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        int l=0,r=n-1,t=0,b=n-1;
        vector<vector<int>> ans(n,vector<int>(n,0));
        int num=1,tar=n*n;
        while(num<=tar)
        {
            for(int i=l;i<=r;i++) ans[t][i]=num++;
            t++;
            for(int i=t;i<=b;i++) ans[i][r]=num++;
            r--;
            for(int i=r;i>=l;i--) ans[b][i]=num++;
            b--;
            for(int i=b;i>=t;i--) ans[i][l]=num++;
            l++;
        }
        return ans;
        
    }
};

//26min  但主要时间是在看大神们的题解
//螺旋矩阵是一个非常经典的题了  我以前的处理方法是设立方向矩阵 力扣官方也是如此
//但是看了k神的题解  发现简洁了太多太多   也非常好记忆与实现
//后续看一下有没有共性  成为通解  如果可以 收货巨大
```
