# 142. 环形链表 II

### 中等
相关标签
相关企业
给定一个链表的头节点  head ，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

如果链表中有某个节点，可以通过连续跟踪 next 指针再次到达，则链表中存在环。 为了表示给定链表中的环，评测系统内部使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。如果 pos 是 -1，则在该链表中没有环。注意：pos 不作为参数进行传递，仅仅是为了标识链表的实际情况。

不允许修改 链表。
```
示例 1：
输入：head = [3,2,0,-4], pos = 1
输出：返回索引为 1 的链表节点
解释：链表中有一个环，其尾部连接到第二个节点
```
![image](https://github.com/user-attachments/assets/7d4e1a79-bc1d-4362-b48e-6f22d2e2fba0)

```
示例 2：
输入：head = [1,2], pos = 0
输出：返回索引为 0 的链表节点
解释：链表中有一个环，其尾部连接到第一个节点。
```
![image](https://github.com/user-attachments/assets/7a7059f1-0ef8-4eaa-9fc5-9ebac1b6af11)

```
示例 3：
输入：head = [1], pos = -1
输出：返回 null
解释：链表中没有环。
 ```
![image](https://github.com/user-attachments/assets/32bb04cf-885d-4f10-b164-c431d44c294d)

提示：

链表中节点的数目范围在范围 [0, 104] 内
-105 <= Node.val <= 105
pos 的值为 -1 或者链表中的一个有效索引
 
进阶：你是否可以使用 O(1) 空间解决此题？

# solution
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        //双指针可以解决吗？
        //看了一下是思路，就是双指针，快慢指针，难点：数学推导
        ListNode* slow=head;
        ListNode* fast=head;
        while(fast!=NULL&&fast->next!=NULL)
        {
            //开始快慢指针 快的一次走两格 慢的一次一格
            slow=slow->next;
            fast=fast->next->next;
            //当相遇时 新定义两个指针 它们再相遇的时候即是环的入口 
            //原因去看代码随想的数学推导
            if(slow==fast)
            {
                ListNode* index1=slow;
                ListNode* index2=head;
                while(index1!=index2)
                {
                    index1=index1->next;
                    index2=index2->next;
                }
                return index1;
            }
        }
        return NULL;
    }
};

//17min   看了一部分思路 剩下自己完成
//这题的代码实现不难  但是思路非常非常难  需要数学推导以发现其中规律
//我想象不出如果没有数学推导发现规律  这题该怎么做  
//但是  我也可以把这题背下来  把相应数学规律背下来   数学规律的具体解释看notes！！

//好的评论：一言以蔽之，相遇之处和链表头距离环入口距离相等
//双指针这个太需要数学推导了，面试手撕怎么办用这个只能靠背把  答：暴力存储所有节点（

//官方有一个用哈希表储存所有节点的   我觉得非常非常不错:

//方法二：哈希表
//思路与算法
//一个非常直观的思路是：我们遍历链表中的每个节点，并将它记录下来；一旦遇到了此前遍历过的节点，就可以判定链表中存在环。借助哈希表可以很方便地实现。
//代码

class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        unordered_set<ListNode *> visited;
        while (head != nullptr) {
            if (visited.count(head)) {
                return head;
            }
            visited.insert(head);
            head = head->next;
        }
        return nullptr;
    }
};

作者：力扣官方题解
链接：https://leetcode.cn/problems/linked-list-cycle-ii/solutions/441131/huan-xing-lian-biao-ii-by-leetcode-solution/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```
