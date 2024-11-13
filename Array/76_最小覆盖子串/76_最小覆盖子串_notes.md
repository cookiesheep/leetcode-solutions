# 两种方法：从 O(52m+n) 到 O(m+n)，附题单（Python/Java/C++/C/Go/JS/Rust）

灵茶山艾府
2022 感恩勋章
49282
2024.03.29
发布于 浙江
数组
字符串
滑动窗口
C
6+
## 前置知识：滑动窗口
如果您不知道滑动窗口，推荐先看视频 滑动窗口【基础算法精讲 03】，并完成 209. 长度最小的子数组 作为本题的铺垫，因为这两题都属于「最短型」滑动窗口。

什么是「涵盖」
看示例 1，s 的子串 BANC 中每个字母的出现次数，都大于等于 t=ABC 中每个字母的出现次数，这就叫涵盖。

## 滑动窗口怎么滑
原理和 209 题一样，按照视频中的做法，我们枚举 s 子串的右端点 right（子串最后一个字母的下标），如果子串涵盖 t，就不断移动左端点 left 直到不涵盖为止。在移动过程中更新最短子串的左右端点。

具体来说：

初始化 ansLeft=−1, ansRight=m，用来记录最短子串的左右端点，其中 m 是 s 的长度。
用一个哈希表（或者数组）cntT 统计 t 中每个字母的出现次数。
初始化 left=0，以及一个空哈希表（或者数组）cntS，用来统计 s 子串中每个字母的出现次数。
遍历 s，设当前枚举的子串右端点为 right，把 s[right] 的出现次数加一。
遍历 cntS 中的每个字母及其出现次数，如果出现次数都大于等于 cntT 中的字母出现次数：
如果 right−left<ansRight−ansLeft，说明我们找到了更短的子串，更新 ansLeft=left, ansRight=right。
把 s[left] 的出现次数减一。
左端点右移，即 left 加一。
重复上述三步，直到 cntS 有字母的出现次数小于 cntT 中该字母的出现次数为止。
最后，如果 ansLeft<0，说明没有找到符合要求的子串，返回空字符串，否则返回下标 ansLeft 到下标 ansRight 之间的子串。
由于本题大写字母和小写字母都有，为了方便，代码实现时可以直接创建大小为 128 的数组，保证所有 ASCII 字符都可以统计。

## 方法一
```cpp
class Solution {
    bool is_covered(int cnt_s[], int cnt_t[]) {
        for (int i = 'A'; i <= 'Z'; i++) {
            if (cnt_s[i] < cnt_t[i]) {
                return false;
            }
        }
        for (int i = 'a'; i <= 'z'; i++) {
            if (cnt_s[i] < cnt_t[i]) {
                return false;
            }
        }
        return true;
    }

public:
    string minWindow(string s, string t) {
        int m = s.length();
        int ans_left = -1, ans_right = m;
        int cnt_s[128]{}; // s 子串字母的出现次数
        int cnt_t[128]{}; // t 中字母的出现次数
        for (char c : t) {
            cnt_t[c]++;
        }

        int left = 0;
        for (int right = 0; right < m; right++) { // 移动子串右端点
            cnt_s[s[right]]++; // 右端点字母移入子串
            while (is_covered(cnt_s, cnt_t)) { // 涵盖
                if (right - left < ans_right - ans_left) { // 找到更短的子串
                    ans_left = left; // 记录此时的左右端点
                    ans_right = right;
                }
                cnt_s[s[left]]--; // 左端点字母移出子串
                left++;
            }
        }
        return ans_left < 0 ? "" : s.substr(ans_left, ans_right - ans_left + 1);
    }
};
```
复杂度分析
时间复杂度：O(∣Σ∣m+n)，其中 m 为 s 的长度，n 为 t 的长度，∣Σ∣ 为字符集合的大小，本题字符均为英文字母，所以 ∣Σ∣=52。注意 left 只会增加不会减少，left 每增加一次，我们就花费 O(∣Σ∣) 的时间。因为 left 至多增加 m 次，所以二重循环的时间复杂度为 O(∣Σ∣m)，再算上统计 t 字母出现次数的时间 O(n)，总的时间复杂度为 O(∣Σ∣m+n)。
空间复杂度：O(∣Σ∣)。如果创建了大小为 128 的数组，则 ∣Σ∣=128。
## 方法二：优化
上面的代码每次都要花费 O(∣Σ∣) 的时间去判断是否涵盖，能不能优化到 O(1) 呢？

可以。用一个变量 less 维护目前子串中有 less 种字母的出现次数小于 t 中字母的出现次数。

### 具体来说（注意下面算法中的 less 变量）：

初始化 ansLeft=−1, ansRight=m，用来记录最短子串的左右端点，其中 m 是 s 的长度。
用一个哈希表（或者数组）cntT 统计 t 中每个字母的出现次数。
初始化 left=0，以及一个空哈希表（或者数组）cntS，用来统计 s 子串中每个字母的出现次数。
初始化 less 为 t 中的不同字母个数。
遍历 s，设当前枚举的子串右端点为 right，把字母 c=s[right] 的出现次数加一。加一后，如果 cntS[c]=cntT[c]，说明 c 的出现次数满足要求，把 less 减一。
如果 less=0，说明 cntS 中的每个字母及其出现次数都大于等于 cntT 中的字母出现次数，那么：
如果 right−left<ansRight−ansLeft，说明我们找到了更短的子串，更新 ansLeft=left, ansRight=right。
把字母 x=s[left] 的出现次数减一。减一前，如果 cntS[x]=cntT[x]，说明 x 的出现次数不满足要求，把 less 加一。
左端点右移，即 left 加一。
重复上述三步，直到 less>0，即 cntS 有字母的出现次数小于 cntT 中该字母的出现次数为止。
最后，如果 ansLeft<0，说明没有找到符合要求的子串，返回空字符串，否则返回下标 ansLeft 到下标 ansRight 之间的子串。
代码实现时，可以把 cntS 和 cntT 合并成一个 cnt，定义

cnt[x]=cntT[x]−cntS[x]
如果 cnt[x]=0，就意味着窗口内字母 x 的出现次数和 t 的一样多。
```cpp
class Solution {
public:
    string minWindow(string s, string t) {
        int m = s.length();
        int ans_left = -1, ans_right = m;
        int cnt[128]{};
        int less = 0;
        for (char c : t) {
            if (cnt[c] == 0) {
                less++; // 有 less 种字母的出现次数 < t 中的字母出现次数
            }
            cnt[c]++;
        }

        int left = 0;
        for (int right = 0; right < m; right++) { // 移动子串右端点
            char c = s[right]; // 右端点字母
            cnt[c]--; // 右端点字母移入子串
            if (cnt[c] == 0) {
                // 原来窗口内 c 的出现次数比 t 的少，现在一样多
                less--;
            }
            while (less == 0) { // 涵盖：所有字母的出现次数都是 >=
                if (right - left < ans_right - ans_left) { // 找到更短的子串
                    ans_left = left; // 记录此时的左右端点
                    ans_right = right;
                }
                char x = s[left]; // 左端点字母
                if (cnt[x] == 0) {
                    // x 移出窗口之前，检查出现次数，
                    // 如果窗口内 x 的出现次数和 t 一样，
                    // 那么 x 移出窗口后，窗口内 x 的出现次数比 t 的少
                    less++;
                }
                cnt[x]++; // 左端点字母移出子串
                left++;
            }
        }
        return ans_left < 0 ? "" : s.substr(ans_left, ans_right - ans_left + 1);
    }
};
```
复杂度分析
时间复杂度：O(m+n) 或 O(m+n+∣Σ∣)，其中 m 为 s 的长度，n 为 t 的长度，∣Σ∣=128。注意 left 只会增加不会减少，二重循环的时间复杂度为 O(m)。使用哈希表写法的时间复杂度为 O(m+n)，数组写法的时间复杂度为 O(m+n+∣Σ∣)。
空间复杂度：O(∣Σ∣)。无论 m 和 n 有多大，额外空间都不会超过 O(∣Σ∣)。
