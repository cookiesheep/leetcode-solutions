# 🧠 解题思路
相信大家看到该题的第一反应应该是使用栈，或者直接删除字符串来解决，但是这样做的话，空间复杂度为： n+m。

这无疑不是更优解，下面，我将介绍一种常量级空间复杂度的解法：双指针，并且比官方解思路更简单清晰！

由于 # 号只会消除左边的一个字符，所以对右边的字符无影响，所以我们选择从后往前遍历 S，T 字符串。

## 思路解析：

准备两个指针 i, j 分别指向 S，T 的末位字符，再准备两个变量 skipS，skipT 来分别存放 S，T 字符串中的 # 数量。
从后往前遍历 S，所遇情况有三，如下所示：
2.1 若当前字符是 #，则 skipS 自增 1；
2.2 若当前字符不是 #，且 skipS 不为 0，则 skipS 自减 1；
2.3 若当前字符不是 #，且 skipS 为 0，则代表当前字符不会被消除，我们可以用来和 T 中的当前字符作比较。
若对比过程出现 S, T 当前字符不匹配，则遍历结束，返回 false，若 S，T 都遍历结束，且都能一一匹配，则返回 true。

文字描述一般在不懂逻辑的时候都比较不容易理解，所以请结合图解来加快理解。


<a>https://pic.leetcode-cn.com/1616899257-WqSIol-9.gif 示意图</a>


```cpp
class Solution {
public:
    bool backspaceCompare(string S, string T) {
        int i = S.length() - 1, j = T.length() - 1;
        int skipS = 0, skipT = 0;

        while (i >= 0 || j >= 0) {
            while (i >= 0) {
                if (S[i] == '#') {
                    skipS++, i--;
                } else if (skipS > 0) {
                    skipS--, i--;
                } else {
                    break;
                }
            }
            while (j >= 0) {
                if (T[j] == '#') {
                    skipT++, j--;
                } else if (skipT > 0) {
                    skipT--, j--;
                } else {
                    break;
                }
            }
            if (i >= 0 && j >= 0) {
                if (S[i] != T[j]) {
                    return false;
                }
            } else {
                if (i >= 0 || j >= 0) {
                    return false;
                }
            }
            i--, j--;
        }
        return true;
    }
};
```
作者：御三五 🥇
链接：https://leetcode.cn/problems/backspace-string-compare/solutions/683776/shuang-zhi-zhen-bi-jiao-han-tui-ge-de-zi-8fn8/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。




作者：御三五 🥇
链接：https://leetcode.cn/problems/backspace-string-compare/solutions/683776/shuang-zhi-zhen-bi-jiao-han-tui-ge-de-zi-8fn8/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
