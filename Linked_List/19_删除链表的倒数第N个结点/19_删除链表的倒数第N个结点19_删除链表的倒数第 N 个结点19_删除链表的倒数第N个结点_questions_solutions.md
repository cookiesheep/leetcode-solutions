# 19. 删除链表的倒数第 N 个结点
已解答
### 中等
相关标签
相关企业
提示
## 给你一个链表，删除链表的倒数第 n 个结点，并且返回链表的头结点。

 
```
示例 1：


输入：head = [1,2,3,4,5], n = 2
输出：[1,2,3,5]
示例 2：

输入：head = [1], n = 1
输出：[]
示例 3：

输入：head = [1,2], n = 1
输出：[1]
 ```

提示：

链表中结点的数目为 sz
1 <= sz <= 30
0 <= Node.val <= 100
1 <= n <= sz


 #  my solutions


 ```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        //目前想到的还是两趟扫描 第一趟算出个数 并得到倒数第n个节点正着数在哪
        if(head==nullptr) return head;
        else if(head->next==nullptr) return nullptr;
        ListNode* cur=head;
        int size=0;
        while(cur!=nullptr)
        {
            cur=cur->next;
            size++;
        }
        cur=head;
        int n2=size-n-1;   //找到要删除的前一个节点
        if(n2<0)  return head->next;       //n2<0意味着删除头节点
        while(n2--&&cur->next!=nullptr)     //头结点难处理
            cur=cur->next;
        if(cur->next==nullptr)
            cur->next=nullptr;
        else  cur->next=cur->next->next;    //链表长度为2 删除最后最后一个时
        return head;
    }
};


//29min             完全独立完成！
//其实挺早就写完了  这题大体上不难 但是有一些细节
//比方说当要删除的是头结点  以及总长度只有2时
//其实我想得不是特别明白  但改着改着莫名其妙就
//    if(n2<0)  return head->next; 这行代码可以处理上面两个问题好像
//思考了一下还是需要添加虚拟头节点最简单  不需要额外判断那么多了
```

# other's solutions

## 前言
### 在对链表进行操作时，一种常用的技巧是添加一个哑节点（dummy node），它的 next 指针指向链表的头节点。这样一来，我们就不需要对头节点进行特殊的判断了。

例如，在本题中，如果我们要删除节点 y，我们需要知道节点 y 的前驱节点 x，并将 x 的指针指向 y 的后继节点。但由于头节点不存在前驱节点，因此我们需要在删除头节点时进行特殊判断。但如果我们添加了哑节点，那么头节点的前驱节点就是哑节点本身，此时我们就只需要考虑通用的情况即可。

特别地，在某些语言中，由于需要自行对内存进行管理。因此在实际的面试中，对于「是否需要释放被删除节点对应的空间」这一问题，我们需要和面试官进行积极的沟通以达成一致。下面的代码中默认不释放空间。

## 方法一：计算链表长度
思路与算法

一种容易想到的方法是，我们首先从头节点开始对链表进行一次遍历，得到链表的长度 L。随后我们再从头节点开始对链表进行一次遍历，当遍历到第 L−n+1 个节点时，它就是我们需要删除的节点。

为了与题目中的 n 保持一致，节点的编号从 1 开始，头节点为编号 1 的节点。

为了方便删除操作，我们可以从哑节点开始遍历 L−n+1 个节点。当遍历到第 L−n+1 个节点时，它的下一个节点就是我们需要删除的节点，这样我们只需要修改一次指针，就能完成删除操作。

```cpp
class Solution {
public:
    int getLength(ListNode* head) {
        int length = 0;
        while (head) {
            ++length;
            head = head->next;
        }
        return length;
    }

    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* dummy = new ListNode(0, head);
        int length = getLength(head);
        ListNode* cur = dummy;
        for (int i = 1; i < length - n + 1; ++i) {
            cur = cur->next;
        }
        cur->next = cur->next->next;
        ListNode* ans = dummy->next;
        delete dummy;
        return ans;
    }
};
//看了一遍 真得方便了特别多！
```
作者：力扣官方题解
链接：https://leetcode.cn/problems/remove-nth-node-from-end-of-list/solutions/450350/shan-chu-lian-biao-de-dao-shu-di-nge-jie-dian-b-61/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
