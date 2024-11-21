# 24. 两两交换链表中的节点
已解答
中等
相关标签
相关企业
## 给你一个链表，两两交换其中相邻的节点，并返回交换后链表的头节点。你必须在不修改节点内部的值的情况下完成本题（即，只能进行节点交换）。

 
```
示例 1：


输入：head = [1,2,3,4]
输出：[2,1,4,3]
示例 2：

输入：head = []
输出：[]
示例 3：

输入：head = [1]
输出：[1]
 ```

提示：

链表中节点的数目在范围 [0, 100] 内
0 <= Node.val <= 100

### 相关标签
递归
链表


# solutions：

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
    ListNode* swapPairs(ListNode* head) {
        if(head==nullptr||head->next==nullptr) return head;
                                //如果是空链表或者只有一个节点
        ListNode* ji=head;      //定义奇数位的指针  一开始先初始化为头指针
        ListNode dummy(0);       //虚拟头节点
        dummy.next=head;
        ListNode* ou1=&dummy;    //定义指向偶数位指针  初始化为head前一个虚拟
        ListNode* ou2=ji->next;
        ListNode* ans=ou2;        
        while(ji!=nullptr&&ou2!=nullptr)
        {
            ListNode* temp=ou2->next;
            ou1->next=ou2;
            ou2->next=ji;         //可以在草稿纸上画一下看看为什么要这么交换
            ji->next=temp;
            ou1=ji;
            ji=temp;
            if(ji!=nullptr)
                ou2=temp->next;
            else ou2=nullptr;
        }
        return ans;
    }
};

//39min    
//算是独立完成！   变量名什么的都是我自己取的  虽然取得很不好
//但是最后还是有一些细节是看了一下gpt  比如终止条件之类的
//但是交换那里的核心代码我一开始就是写对的
//不过写得还是太不清晰了  我感觉我下次看就会看不懂了...
```

# gpt给的代码：
```cpp
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if (head == nullptr || head->next == nullptr) return head; // 链表为空或只有一个节点直接返回
        
        ListNode dummy(0); // 创建一个虚拟节点，方便操作
        dummy.next = head;
        ListNode* prev = &dummy; // 指向交换节点前的位置
        
        while (prev->next != nullptr && prev->next->next != nullptr) {
            ListNode* first = prev->next;        // 第一个节点
            ListNode* second = prev->next->next; // 第二个节点
            
            // 交换节点
            first->next = second->next;
            second->next = first;
            prev->next = second;
            
            // 移动到下一个需要交换的位置
            prev = first;
        }
        
        return dummy.next;
    }
};

```
