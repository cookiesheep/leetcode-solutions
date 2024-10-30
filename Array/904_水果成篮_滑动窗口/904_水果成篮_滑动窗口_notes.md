# 解题思路
出发点是追求通法，笔者刚刚做完了76题。毫无疑问，这道题也是用滑动窗口的，lc.76也使用滑动窗口。但很奇怪，笔者在很快做出76题后，惊讶的发现在这道题76题的思路并不适用？！76题极简代码、思路

同样是滑动窗口，这两题有什么区别？区别在于76题求的是最小滑窗，而本题求的是最大滑窗。

# 最小滑窗模板：给定数组 nums，定义滑窗的左右边界 i, j，求满足某个条件的滑窗的最小长度。
```cpp
while j < len(nums):
    判断[i, j]是否满足条件
    while 满足条件：
        不断更新结果(注意在while内更新！)
        i += 1 （最大程度的压缩i，使得滑窗尽可能的小）
    j += 1
# 最大滑窗模板：给定数组 nums，定义滑窗的左右边界 i, j，求满足某个条件的滑窗的最大长度。
while j < len(nums):
    判断[i, j]是否满足条件
    while 不满足条件：
        i += 1 （最保守的压缩i，一旦满足条件了就退出压缩i的过程，使得滑窗尽可能的大）
    不断更新结果（注意在while外更新！）
    j += 1
```
## 是的，关键的区别在于，最大滑窗是在迭代右移右边界的过程中更新结果，而最小滑窗是在迭代右移左边界的过程中更新结果。
因此虽然都是滑窗，但是两者的模板和对应的贪心思路并不一样，而真正理解后就可以在lc.76，lc.904，lc.3, lc.1004写出非常无脑的代码。

时间复杂度为：O(N), 空间复杂度为：O(N).

## 其实双指针和滑动窗口是有些许区别的。
滑动窗口一句话就是右指针先出发，左指针视情况追赶右指针。可类比男生暗恋女生，两人都在往前走，但男生总是默默跟着女生走但又不敢超过她。因此，右指针最多遍历一遍数组，左指针也最多遍历一次数组，时间复杂度不超过O(2N)。接下来，如何判断滑动窗口内是否满足题设条件，有两种选择：(1) 要么你遍历这个滑窗，通过遍历来断滑窗是否满足需要O(N), 那么总的时间就退化为O(N^2), (2) 要么你选择字典，用空间换时间，那么判断划窗是否满足条件则需要 O(1)，总时间为O(N).

## lc904 水果成篮（最大滑窗）
白话题意：求满足某个条件（数组值最多就两类的连续数组，例如[1,2,2,1,2]）的最长数组长度
```python
class Solution:
    def totalFruit(self, fruits: List[int]) -> int:
        # 初始化
        i, j = 0, 0
        res = 0
        classMap = defaultdict(int)
        classCnt = 0
        
        # 移动滑窗右边界 
        while j < len(fruits):
            # 判断当前是否满足条件
            if classMap[fruits[j]] == 0:
                classCnt += 1
            classMap[fruits[j]] += 1

            # 若不满足条件，移动i
            while classCnt > 2:
                if classMap[fruits[i]] == 1:
                    classCnt -= 1
                classMap[fruits[i]] -= 1
                i += 1

            # 一旦满足条件，更新结果
            res = max(res, j - i + 1)
            j += 1
        return res
```
## lc76 最小覆盖子串（最小滑窗）
```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        # 初始化
        i, j = 0, 0
        needMap = collections.defaultdict(int)
        needCnt = len(t)
        res = ''
        
        for char in t:
            needMap[char] += 1

        # 移动滑窗右边界
        while j < len(s):
            # 判断是否满足条件
            if s[j] in needMap:
                if needMap[s[j]] > 0:
                    needCnt -= 1
                needMap[s[j]] -= 1

            # 一旦满足条件，尽可能的压缩i，并且不断更新结果。
            while needCnt == 0:
                #print(i, j)
                if not res or j - i + 1 < len(res):
                    res = s[i:j+1]

                if s[i] in needMap:
                    if needMap[s[i]] == 0:
                        needCnt += 1
                    needMap[s[i]] += 1
                i += 1

            j += 1
        return res 
```
其他滑动窗口模板题:
## lc.1004 最大连续1的个数 III
```python
class Solution:
    def longestOnes(self, nums: List[int], k: int) -> int:

        res = 0
        i, j = 0, 0
        zeroCnt = 0

        while j < len(nums):

            if nums[j] == 0:
                zeroCnt += 1

            while zeroCnt > k:
                if nums[i] == 0:
                    zeroCnt -= 1
                i += 1

            res = max(res, j - i + 1)
            j += 1
        return res
是的，这不就是最大滑窗吗？秒做！
```
## lc3. 无重复字符的最长子串
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        i, j = 0, 0
        res = 0
        dic = collections.defaultdict(int)
        
        while j < len(s):
            dic[s[j]] += 1

            while len(dic) < j - i + 1:
                dic[s[i]] -= 1
                if dic[s[i]] == 0:
                    del dic[s[i]]
                i += 1

            if len(dic) == j - i + 1:
                res = max(res, j - i + 1)
            j += 1
        return res
```
还是最大滑窗，实际上这道题的判断条件可以进行优化，但是为了满足模板的统一，因此使用了字典的操作，这样做的好处在于代码结构和最大滑窗模板一模一样。

作者：HelloPGJC
链接：https://leetcode.cn/problems/fruit-into-baskets/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
