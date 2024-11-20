# 206. 反转链表
已解答
### 简单
相关标签
相关企业
## 给你单链表的头节点 head ，请你反转链表，并返回反转后的链表。
 
```
示例 1：


输入：head = [1,2,3,4,5]
输出：[5,4,3,2,1]
示例 2：


输入：head = [1,2]
输出：[2,1]
示例 3：

输入：head = []
输出：[]
 ```

提示：

链表中节点的数目范围是 [0, 5000]
-5000 <= Node.val <= 5000
 

进阶：链表可以选用迭代或递归方式完成反转。你能否用两种方法解决这道题？





# solution:
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
    ListNode* reverseList(ListNode* head) {
        ListNode* cur=head;
        ListNode* pre=nullptr;
        while(cur!=nullptr)
        {
            ListNode* temp=cur->next;     //先保存一下先一个节点
                                          //因为等下要反转了 指不到他了
            cur->next=pre;                //反转完成
            pre=cur;                      //pre和cur向后移动
            cur=temp;
        }
        return pre;
    }
};

//15min  
//算是独立完成吧   一开始定义的是cur与nex算不下去
//看了一眼解析改用了cur与pre
```
