# 242. 有效的字母异位词

### 简单
### 相关标签:哈希表 字符串 排序
相关企业
给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的 
字母异位词。
```
示例 1:

输入: s = "anagram", t = "nagaram"
输出: true
示例 2:

输入: s = "rat", t = "car"
输出: false
 ```

提示:

1 <= s.length, t.length <= 5 * 104
s 和 t 仅包含小写字母
 

进阶: 如果输入字符串包含 unicode 字符怎么办？你能否调整你的解法来应对这种情况？

# solutions
```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        if(t.size()!=s.size()) return false;
        unordered_multiset<char> myset1;      //要可以重复的
        unordered_multiset<char> myset2;
        for(int i=0;i<s.size();i++)
            myset1.insert(s[i]);
        for(int i=0;i<t.size();i++)
            myset2.insert(t[i]);
                
        for(const auto& elem : myset2)          //很重要！！！
        {   
            if(myset1.find(elem)==myset1.end())
                return false;
            if(myset1.count(elem)!=myset2.count(elem))   
                return false;                   
        }                        
        return true;
    }
};
//30min   题目不难  但是花了一些时间学习这个新的数据结构
//哈希表还是挺不一样的   有好多要注意的点
// 1. for(const auto& elem : myset2)这个遍历很有讲究   因为这个是无序的 所以不能用下表访问
//     而这句话的含义是：auto&：auto：自动推导变量的类型。
//     在这个例子中，auto 会被推导为 unordered_multiset<char> 中的元素类型（即 char）。
//     &（引用）：表示不拷贝容器中的元素，而是通过引用访问元素。
//     elem：每次迭代中，elem 是当前遍历到的容器元素。
//     myset2：容器对象（unordered_multiset<char>）for 循环会遍历 myset2 中的每个元素
// 2. find函数：find 函数不会返回一个布尔而是返回一个迭代器。如果键存在，它返回指向该键的迭代 
//     器；如果键不存在，它返回 end()
// 3. unordered_multiset表述元素是可以重复的
// 4. insert函数表示插入
    ```
