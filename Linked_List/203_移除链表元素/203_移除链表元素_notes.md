# 【套路】如何优雅地删除链表节点？（Python/Java/C++/C/Go/JS/Rust）

灵茶山艾府
2022 感恩勋章
6045
2024.06.10
发布于 浙江
链表
C
C++
Go
4+
## 套路 1
要想删除节点 node，必须在 node 的前一个节点执行删除操作。

例如链表 1→2→3，要想删除 2，必须在节点 1 处操作，也就是把节点 1 的 next 更新为节点 3。

## 套路 2
### 不在需要单独判断头节点
如果头节点可能被删除，那么要在头节点之前添加一个哨兵节点，这样我们无需特判头节点被删除的情况，从而简化代码逻辑。

或者说，根据套路 1，要想删除头节点，必须在头节点的前一个节点操作，所以要添加一个哨兵节点。

### 算法
初始化哨兵节点 dummy，其 next 为 head。
遍历链表，初始化 cur=dummy。
循环直到 cur 的下一个节点为空。
如果 cur 的下一个节点的值等于 val，那么删除下一个节点，把 cur.next 更新为 cur.next.next。
如果 cur 的下一个节点的值不等于 val，那么不删除下一个节点，继续看下下一个节点是否要删除，即更新 cur 为 cur.next。
循环结束，返回 dummy.next，即删除节点后的新链表的头节点。
### 答疑
问：为什么没有修改 dummy，但 dummy.next 却是新链表的头节点？如果删除了 head，那么最后返回的是不是原链表的头节点？

答：注意初始化时，cur 和 dummy 都指向同一个节点，cur 和 dummy 只是同一个节点的引用，所以修改 cur.next 也会同时修改 dummy.next。

问：为什么删除下一个节点后，不需要更新 cur 为 cur.next？

答：删除下一个节点后，cur.next 的节点值也可能等于 val，也需要删除，如果直接更新 cur 为 cur.next，就漏删了节点。
```cpp
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        ListNode dummy(0, head);
        auto cur = &dummy;
        while (cur->next) {
            auto nxt = cur->next;
            if (nxt->val == val) {
                cur->next = nxt->next;
                delete nxt; // 删除下一个节点
            } else {
                cur = nxt; // 继续向后遍历链表
            }
        }
        return dummy.next;
    }
};
```
复杂度分析
时间复杂度：O(n)，其中 n 是链表的长度。
空间复杂度：O(1)
