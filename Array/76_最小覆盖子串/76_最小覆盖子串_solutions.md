```cpp
// 一开始这个是自己想的  时间太慢了
// class Solution {
// public:
//     string minWindow(string s, string t) {
//         sort(t.begin(),t.end());
//         int i=0;
//         string ans=s,zichuan="";
//         for(int j=0;j<s.size();j++)
//         {
//             zichuan+=s[j];
//             string temp=zichuan;
//             sort(temp.begin(),temp.end());
//             while(temp.find(t) != string::npos)
//             {
//                 zichuan.erase(0,1);
//                 i++;
//                 if(ans.size()>zichuan.size())
//                     ans=zichuan;
//             }
//         }
//         return ans==s?"":ans;
//     }
// };



class Solution {
    bool is_hangai(int cnts[],int cntt[])       //判断是否涵盖的函数
    {
        for(int i='A';i<='Z';i++)
        {
            if(cnts[i]<cntt[i]) 
                return false;//目前s中出现的次数比子串少，未涵盖
        }
        for(int i='a';i<='z';i++)
        {
            if(cnts[i]<cntt[i]) 
                return false;//目前s中出现的次数比子串少，未涵盖
        }
        return true;
    }
public:
    string minWindow(string s, string t) {
        int m=s.size();
        int ansleft=-1,ansright=m;
        int cnts[128]{};
        int cntt[128]{};            //统计c，t字符串中个字母出现次数
        for(char c:t)               //遍历一个字符串的方法  值得学习！
        {
            cntt[c]++;              //统计t中所有字母数量   
        }
        int left=0;                 //左指针
        for(int right=0;right<m;right++)    //滑动窗口常遍历终点位置
        {
            cnts[s[right]]++;       //将s右端点字母移入判断数组
            while(is_hangai(cnts,cntt))     //滑动窗口代码核心：窗口变化
            {
                if(right-left<ansright-ansleft)     //找最小窗口
                {
                    ansleft=left;
                    ansright=right;
                }
                cnts[s[left]]--;    //左端字母移出  因为缩小了窗口
                left++;
            }
        }
        return ansleft<0?"":s.substr(ansleft,ansright-ansleft+1);  
                                    //倘若最后长度小于0，说明没有找到
    }
};

//用时29min     算上了看解析    其实这题断断续续得做了好久   中间可能隔了一周多
//真正去写发现也没有那么那么难（虽然看了解析） 所以以后不要畏难  慢慢啃 是一定可以的
```
