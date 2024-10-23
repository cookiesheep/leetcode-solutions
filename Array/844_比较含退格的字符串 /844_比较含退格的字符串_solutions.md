```cpp

class Solution {
public:
    bool backspaceCompare(string s, string t) {
        int i=s.size()-1,j=t.size()-1;
        int skips=0,skipt=0;
        while(i>=0||j>=0)
        {
            while(i>=0)
            {
                if(s[i]=='#')
                {
                    skips++;
                    i--;
                }
                else if(skips>0)
                {
                    skips--;
                    i--;
                }
                else break;
            }
            while(j>=0)
            {
                if(t[j]=='#')
                {
                    skipt++;
                    j--;
                }
                else if(skipt>0)
                {
                    skipt--;
                    j--;
                }
                else break;
            }
            if(i>=0&&j>=0)
            {
                if(s[i]!=t[j])
                return 0;
            }
            else 
                if(i>=0||j>=0)
                return 0;
        
            i--;j--;
        }
        return 1;
    }
};
//双指针  从后往前
//思想：每碰到一个#后skip+1  当skip不为0时，当前位的字符不用比较
//不是自己做出来的 想了挺久没想到


//solution 2:栈
class Solution {
public:
    bool backspaceCompare(string s, string t) {
        return rebuild(s)==rebuild(t);
    }
    string rebuild(string str)
    {
        string news;
        for(int i=0;i<str.size();i++)
        {
            if(str[i]!='#')
                news.push_back(str[i]);
            else if(!news.empty())
                news.pop_back();
        }
        return news;
    }
};

//这个方法用得更舒服一些  清晰明了
```
