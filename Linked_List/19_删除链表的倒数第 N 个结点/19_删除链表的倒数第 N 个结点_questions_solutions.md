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
```
