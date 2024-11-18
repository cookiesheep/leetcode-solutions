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
    ListNode* removeElements(ListNode* head, int val) {
        if(head==nullptr)  return head;         //这意味着空指针

        while(head!=nullptr&&head->val==val)
        {
            ListNode* temp=head;
            head=head->next;
            delete temp;
        }                       //处理头节点  这一步必不可少  
                                //如果头节点就是要删掉的 不进行这步删不掉
                                //题解有另外的方法

        ListNode* ptr=head;
        while(ptr!=nullptr&&ptr->next!=nullptr)
        {
            if(ptr->next->val==val)  
            {
                ListNode* temp=ptr->next;
                ptr->next=ptr->next->next;
                delete temp;
            }
            else ptr=ptr->next;
        }
        return head;
    }
};

//26min   
//期间花了一些时间问gpt 如何遍历指针与删除元素
//我觉得以前的记忆找回了一点





// 方法一：递归
// 链表的定义具有递归的性质，因此链表题目常可以用递归的方法求解。这道题要求删除链表中所有节点值等于特定值的节点，可以用递归实现。

// 对于给定的链表，首先对除了头节点 head 以外的节点进行删除操作，然后判断 head 的节点值是否等于给定的 val。如果 head 的节点值等于 val，则 head 需要被删除，因此删除操作后的头节点为 head.next；如果 head 的节点值不等于 val，则 head 保留，因此删除操作后的头节点还是 head。上述过程是一个递归的过程。

// 递归的终止条件是 head 为空，此时直接返回 head。当 head 不为空时，递归地进行删除操作，然后判断 head 的节点值是否等于 val 并决定是否要删除 head。

// Java
// C#
// JavaScript
// Golang
// C++
// C
// class Solution {
// public:
//     ListNode* removeElements(ListNode* head, int val) {
//         if (head == nullptr) {
//             return head;
//         }
//         head->next = removeElements(head->next, val);
//         return head->val == val ? head->next : head;
//     }
// };
// 复杂度分析

// 时间复杂度：O(n)，其中 n 是链表的长度。递归过程中需要遍历链表一次。

// 空间复杂度：O(n)，其中 n 是链表的长度。空间复杂度主要取决于递归调用栈，最多不会超过 n 层。

// 作者：力扣官方题解
// 链接：https://leetcode.cn/problems/remove-linked-list-elements/solutions/813358/yi-chu-lian-biao-yuan-su-by-leetcode-sol-654m/
// 来源：力扣（LeetCode）
// 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```
