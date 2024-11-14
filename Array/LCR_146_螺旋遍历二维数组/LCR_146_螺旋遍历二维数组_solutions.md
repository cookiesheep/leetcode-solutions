```cpp
class Solution {
public:
    vector<int> spiralArray(vector<vector<int>>& array) {
        if (array.empty()) return {};
        int m=array.size();
        int n=array[0].size();
        int l=0,r=n-1,t=0,b=m-1;
        vector<int> ans;
        while(1)
        {
            for(int i=l;i<=r;i++) ans.push_back(array[t][i]);
            if(++t>b)  break;
            for(int i=t;i<=b;i++) ans.push_back(array[i][r]);
            if(--r<l)  break;
            for(int i=r;i>=l;i--) ans.push_back(array[b][i]);
            if(--b<t)  break;
            for(int i=b;i>=t;i--) ans.push_back(array[i][l]);
            if(++l>r)  break; 
        }
        return ans;
    }   
};

//14 min     和昨天敲过的一样  不过又复习一遍
```
