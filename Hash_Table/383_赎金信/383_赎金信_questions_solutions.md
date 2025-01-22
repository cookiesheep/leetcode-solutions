# 383. 赎金信
已解答
## 简单
## 相关标签：哈希表
给你两个字符串：ransomNote 和 magazine ，判断 ransomNote 能不能由 magazine 里面的字符构成。

如果可以，返回 true ；否则返回 false 。

magazine 中的每个字符只能在 ransomNote 中使用一次。

 
```
示例 1：

输入：ransomNote = "a", magazine = "b"
输出：false
```
```
示例 2：

输入：ransomNote = "aa", magazine = "ab"
输出：false
```
```
示例 3：

输入：ransomNote = "aa", magazine = "aab"
输出：true
 ```
提示：
1 <= ransomNote.length, magazine.length <= 105
ransomNote 和 magazine 由小写英文字母组成

# solutions:
```cpp
class Solution {
public:
    bool canConstruct(string ransomNote, string magazine) {
        //判断：可以重复  无序  用unordered_multiset
        unordered_multiset<char> set1;
        unordered_multiset<char> set2;
        for(int i=0;i<ransomNote.size();i++)
            set1.insert(ransomNote[i]);
        for(int i=0;i<magazine.size();i++)
            set2.insert(magazine[i]);
        for(const auto& i : set1)
        {
            if(set2.find(i)==set2.end())
                return false;
            else 
            {
            // 在magazin找到值为 ransomnote(i)的第一个位置，并删除，表示用掉了这一个值
                auto it = set2.find(i);  // 找到第一个为该值的迭代器
                set2.erase(it);
            }
            // if(set1.count(i)<set2.count(i))   
            //     return false; 
        }
        return true;
    }
};

// 不算难 29min  和242. 有效的字母异位词这题非常像
// 有两种思路：第一种：每找到一个字符在set2中把它删去  表示用用掉它了
//            第二种：直接比较字符的数目，用count函数

```
