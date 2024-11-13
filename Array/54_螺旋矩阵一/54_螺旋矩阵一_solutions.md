```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int m = matrix.size();
        if (m == 0) return {};  // 如果矩阵为空，返回空向量
        int n = matrix[0].size();  // 读取矩阵的列数

        int l = 0, r = n - 1, t = 0, b = m - 1;
        int num = 0, tar = m * n;
        vector<int> ans(tar);

        while (num < tar) {
            // 从左到右
            for (int i = l; i <= r && num < tar; i++) 
                ans[num++] = matrix[t][i];
            t++;
            // 从上到下
            for (int i = t; i <= b && num < tar; i++) 
                ans[num++] = matrix[i][r];
            r--;
            // 从右到左
            for (int i = r; i >= l && num < tar; i--) 
                ans[num++] = matrix[b][i];
            b--;
            // 从下到上
            for (int i = b; i >= t && num < tar; i--) 
                ans[num++] = matrix[i][l];
            l++;
        }

        return ans;
    }
};

//30min    本来以为很简单 第一遍敲完只用了5-8min  但是后面疯狂出bug
//原因：有坑  没有上一题那么简单  非常容易越界
//必须在每个for循环加上边界检查： && num < tar
//我一开始是用if边界检查  不知道哪里出问题了    if(num+1<=tar) num++;else break;
//最后是是靠gpt写出来的
```
### 后面去看了一下看k神的，感觉人家写得好多了，直接放在下面：
```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        if (matrix.empty()) return {};
        int l = 0, r = matrix[0].size() - 1, t = 0, b = matrix.size() - 1;
        vector<int> res;
        while (true) {
            for (int i = l; i <= r; i++) res.push_back(matrix[t][i]); // left to right
            if (++t > b) break;
            for (int i = t; i <= b; i++) res.push_back(matrix[i][r]); // top to bottom
            if (l > --r) break;
            for (int i = r; i >= l; i--) res.push_back(matrix[b][i]); // right to left
            if (t > --b) break;
            for (int i = b; i >= t; i--) res.push_back(matrix[i][l]); // bottom to top
            if (++l > r) break;
        }
        return res;
    }
};

作者：Krahets
链接：https://leetcode.cn/problems/spiral-matrix/solutions/2362055/54-luo-xuan-ju-zhen-mo-ni-qing-xi-tu-jie-juvi/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```
