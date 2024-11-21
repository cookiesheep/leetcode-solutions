# 算法公开课
《代码随想录》算法视频公开课 (opens new window)：帮你把链表细节学清楚！ | LeetCode：24. 两两交换链表中的节点 (opens new window)，相信结合视频再看本篇题解，更有助于大家对本题的理解。

# 思路
这道题目正常模拟就可以了。

建议使用虚拟头结点，这样会方便很多，要不然每次针对头结点（没有前一个指针指向头结点），还要单独处理。

对虚拟头结点的操作，还不熟悉的话，可以看这篇链表：听说用虚拟头节点会方便很多？ (opens new window)。

接下来就是交换相邻两个元素了，此时一定要画图，不画图，操作多个指针很容易乱，而且要操作的先后顺序

初始时，cur指向虚拟头结点，然后进行如下三步：

![image](https://github.com/user-attachments/assets/9d5eafd3-2c22-4379-a442-a75337d97b26)


操作之后，链表如下：

![image](https://github.com/user-attachments/assets/2565aee3-18f9-4472-a3c0-8c6978dc932f)


看这个可能就更直观一些了：

![image](https://github.com/user-attachments/assets/82e22e92-b92d-49a6-904d-5a0fe318a5bd)


对应的C++代码实现如下： （注释中详细和如上图中的三步做对应）
```cpp
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        ListNode* dummyHead = new ListNode(0); // 设置一个虚拟头结点
        dummyHead->next = head; // 将虚拟头结点指向head，这样方便后面做删除操作
        ListNode* cur = dummyHead;
        while(cur->next != nullptr && cur->next->next != nullptr) {
            ListNode* tmp = cur->next; // 记录临时节点
            ListNode* tmp1 = cur->next->next->next; // 记录临时节点

            cur->next = cur->next->next;    // 步骤一
            cur->next->next = tmp;          // 步骤二
            cur->next->next->next = tmp1;   // 步骤三

            cur = cur->next->next; // cur移动两位，准备下一轮交换
        }
        ListNode* result = dummyHead->next;
        delete dummyHead;
        return result;
    }
};
```
时间复杂度：O(n)
空间复杂度：O(1)


# 方法二：递归
思路与算法

可以通过递归的方式实现两两交换链表中的节点。

递归的终止条件是链表中没有节点，或者链表中只有一个节点，此时无法进行交换。

如果链表中至少有两个节点，则在两两交换链表中的节点之后，原始链表的头节点变成新的链表的第二个节点，原始链表的第二个节点变成新的链表的头节点。链表中的其余节点的两两交换可以递归地实现。在对链表中的其余节点递归地两两交换之后，更新节点之间的指针关系，即可完成整个链表的两两交换。

用 head 表示原始链表的头节点，新的链表的第二个节点，用 newHead 表示新的链表的头节点，原始链表的第二个节点，则原始链表中的其余节点的头节点是 newHead.next。令 head.next = swapPairs(newHead.next)，表示将其余节点进行两两交换，交换后的新的头节点为 head 的下一个节点。然后令 newHead.next = head，即完成了所有节点的交换。最后返回新的链表的头节点 newHead。

代码

Java
C++
JavaScript
Python3
Golang
C
```cpp
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if (head == nullptr || head->next == nullptr) {
            return head;
        }
        ListNode* newHead = head->next;
        head->next = swapPairs(newHead->next);
        newHead->next = head;
        return newHead;
    }
};
```
复杂度分析

时间复杂度：O(n)，其中 n 是链表的节点数量。需要对每个节点进行更新指针的操作。

空间复杂度：O(n)，其中 n 是链表的节点数量。空间复杂度主要取决于递归调用的栈空间。

作者：力扣官方题解
链接：https://leetcode.cn/problems/swap-nodes-in-pairs/solutions/444474/liang-liang-jiao-huan-lian-biao-zhong-de-jie-di-91/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
