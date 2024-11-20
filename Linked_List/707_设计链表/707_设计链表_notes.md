题意：

在链表类中实现这些功能：

get(index)：获取链表中第 index 个节点的值。如果索引无效，则返回-1。
addAtHead(val)：在链表的第一个元素之前添加一个值为 val 的节点。插入后，新节点将成为链表的第一个节点。
addAtTail(val)：将值为 val 的节点追加到链表的最后一个元素。
addAtIndex(index,val)：在链表中的第 index 个节点之前添加值为 val  的节点。如果 index 等于链表的长度，则该节点将附加到链表的末尾。如果 index 大于链表长度，则不会插入节点。如果index小于0，则在头部插入节点。
deleteAtIndex(index)：如果索引 index 有效，则删除链表中的第 index 个节点。
# 707示例

# 算法公开课
《代码随想录》算法视频公开课 (opens new window)：帮你把链表操作学个通透！LeetCode：707.设计链表 (opens new window)，相信结合视频再看本篇题解，更有助于大家对本题的理解。

# 思路
如果对链表的基础知识还不太懂，可以看这篇文章：关于链表，你该了解这些！(opens new window)

如果对链表的虚拟头结点不清楚，可以看这篇文章：链表：听说用虚拟头节点会方便很多？(opens new window)

删除链表节点： 链表-删除节点

添加链表节点： 链表-添加节点

这道题目设计链表的五个接口：

获取链表第index个节点的数值
在链表的最前面插入一个节点
在链表的最后面插入一个节点
在链表第index个节点前面插入一个节点
删除链表的第index个节点
可以说这五个接口，已经覆盖了链表的常见操作，是练习链表操作非常好的一道题目

## 链表操作的两种方式：

### 直接使用原来的链表来进行操作。
### 设置一个虚拟头结点在进行操作。
下面采用的设置一个虚拟头结点（这样更方便一些，大家看代码就会感受出来）。
```cpp
class MyLinkedList {
public:
    // 定义链表节点结构体
    struct LinkedNode {
        int val;
        LinkedNode* next;
        LinkedNode(int val):val(val), next(nullptr){}
    };

    // 初始化链表
    MyLinkedList() {
        _dummyHead = new LinkedNode(0); // 这里定义的头结点 是一个虚拟头结点，而不是真正的链表头结点
        _size = 0;
    }

    // 获取到第index个节点数值，如果index是非法数值直接返回-1， 注意index是从0开始的，第0个节点就是头结点
    int get(int index) {
        if (index > (_size - 1) || index < 0) {
            return -1;
        }
        LinkedNode* cur = _dummyHead->next;
        while(index--){ // 如果--index 就会陷入死循环
            cur = cur->next;
        }
        return cur->val;
    }

    // 在链表最前面插入一个节点，插入完成后，新插入的节点为链表的新的头结点
    void addAtHead(int val) {
        LinkedNode* newNode = new LinkedNode(val);
        newNode->next = _dummyHead->next;
        _dummyHead->next = newNode;
        _size++;
    }

    // 在链表最后面添加一个节点
    void addAtTail(int val) {
        LinkedNode* newNode = new LinkedNode(val);
        LinkedNode* cur = _dummyHead;
        while(cur->next != nullptr){
            cur = cur->next;
        }
        cur->next = newNode;
        _size++;
    }

    // 在第index个节点之前插入一个新节点，例如index为0，那么新插入的节点为链表的新头节点。
    // 如果index 等于链表的长度，则说明是新插入的节点为链表的尾结点
    // 如果index大于链表的长度，则返回空
    // 如果index小于0，则在头部插入节点
    void addAtIndex(int index, int val) {

        if(index > _size) return;
        if(index < 0) index = 0;        
        LinkedNode* newNode = new LinkedNode(val);
        LinkedNode* cur = _dummyHead;
        while(index--) {
            cur = cur->next;
        }
        newNode->next = cur->next;
        cur->next = newNode;
        _size++;
    }

    // 删除第index个节点，如果index 大于等于链表的长度，直接return，注意index是从0开始的
    void deleteAtIndex(int index) {
        if (index >= _size || index < 0) {
            return;
        }
        LinkedNode* cur = _dummyHead;
        while(index--) {
            cur = cur ->next;
        }
        LinkedNode* tmp = cur->next;
        cur->next = cur->next->next;
        delete tmp;
        //delete命令指示释放了tmp指针原本所指的那部分内存，
        //被delete后的指针tmp的值（地址）并非就是NULL，而是随机值。也就是被delete后，
        //如果不再加上一句tmp=nullptr,tmp会成为乱指的野指针
        //如果之后的程序不小心使用了tmp，会指向难以预想的内存空间
        tmp=nullptr;
        _size--;
    }

    // 打印链表
    void printLinkedList() {
        LinkedNode* cur = _dummyHead;
        while (cur->next != nullptr) {
            cout << cur->next->val << " ";
            cur = cur->next;
        }
        cout << endl;
    }
private:
    int _size;
    LinkedNode* _dummyHead;

};
```
时间复杂度: 涉及 index 的相关操作为 O(index), 其余为 O(1)
空间复杂度: O(n)
#其他语言版本
# C++双链表法:
## 重点看一下这个方法 这个当初我没有实现
```cpp
//采用循环虚拟结点的双链表实现
class MyLinkedList {
public:
    // 定义双向链表节点结构体
    struct DList {
        int elem; // 节点存储的元素
        DList *next; // 指向下一个节点的指针
        DList *prev; // 指向上一个节点的指针
        // 构造函数，创建一个值为elem的新节点
        DList(int elem) : elem(elem), next(nullptr), prev(nullptr) {};
    };

    // 构造函数，初始化链表
    MyLinkedList() {
        sentinelNode = new DList(0); // 创建哨兵节点，不存储有效数据
        sentinelNode->next = sentinelNode; // 哨兵节点的下一个节点指向自身，形成循环
        sentinelNode->prev = sentinelNode; // 哨兵节点的上一个节点指向自身，形成循环
        size = 0; // 初始化链表大小为0
    }

    // 获取链表中第index个节点的值
    int get(int index) {
        if (index > (size - 1) || index < 0) { // 检查索引是否超出范围
            return -1; // 如果超出范围，返回-1
        }
        int num;
        int mid = size >> 1; // 计算链表中部位置
        DList *curNode = sentinelNode; // 从哨兵节点开始
        if (index < mid) { // 如果索引小于中部位置，从前往后遍历
            for (int i = 0; i < index + 1; i++) {
                curNode = curNode->next; // 移动到目标节点
            }
        } else { // 如果索引大于等于中部位置，从后往前遍历
            for (int i = 0; i < size - index; i++) {
                curNode = curNode->prev; // 移动到目标节点
            }
        }
        num = curNode->elem; // 获取目标节点的值
        return num; // 返回节点的值
    }

    // 在链表头部添加节点
    void addAtHead(int val) {
        DList *newNode = new DList(val); // 创建新节点
        DList *next = sentinelNode->next; // 获取当前头节点的下一个节点
        newNode->prev = sentinelNode; // 新节点的上一个节点指向哨兵节点
        newNode->next = next; // 新节点的下一个节点指向原来的头节点
        size++; // 链表大小加1
        sentinelNode->next = newNode; // 哨兵节点的下一个节点指向新节点
        next->prev = newNode; // 原来的头节点的上一个节点指向新节点
    }

    // 在链表尾部添加节点
    void addAtTail(int val) {
        DList *newNode = new DList(val); // 创建新节点
        DList *prev = sentinelNode->prev; // 获取当前尾节点的上一个节点
        newNode->next = sentinelNode; // 新节点的下一个节点指向哨兵节点
        newNode->prev = prev; // 新节点的上一个节点指向原来的尾节点
        size++; // 链表大小加1
        sentinelNode->prev = newNode; // 哨兵节点的上一个节点指向新节点
        prev->next = newNode; // 原来的尾节点的下一个节点指向新节点
    }

    // 在链表中的第index个节点之前添加值为val的节点
    void addAtIndex(int index, int val) {
        if (index > size) { // 检查索引是否超出范围
            return; // 如果超出范围，直接返回
        }
        if (index <= 0) { // 如果索引为0或负数，在头部添加节点
            addAtHead(val);
            return;
        }
        int num;
        int mid = size >> 1; // 计算链表中部位置
        DList *curNode = sentinelNode; // 从哨兵节点开始
        if (index < mid) { // 如果索引小于中部位置，从前往后遍历
            for (int i = 0; i < index; i++) {
                curNode = curNode->next; // 移动到目标位置的前一个节点
            }
            DList *temp = curNode->next; // 获取目标位置的节点
            DList *newNode = new DList(val); // 创建新节点
            curNode->next = newNode; // 在目标位置前添加新节点
            temp->prev = newNode; // 目标位置的节点的前一个节点指向新节点
            newNode->next = temp; // 新节点的下一个节点指向目标位置的结点
            newNode->prev = curNode; // 新节点的上一个节点指向当前节点
        } else { // 如果索引大于等于中部位置，从后往前遍历
            for (int i = 0; i < size - index; i++) {
                curNode = curNode->prev; // 移动到目标位置的后一个节点
            }
            DList *temp = curNode->prev; // 获取目标位置的节点
            DList *newNode = new DList(val); // 创建新节点
            curNode->prev = newNode; // 在目标位置后添加新节点
            temp->next = newNode; // 目标位置的节点的下一个节点指向新节点
            newNode->prev = temp; // 新节点的上一个节点指向目标位置的节点
            newNode->next = curNode; // 新节点的下一个节点指向当前节点
        }
        size++; // 链表大小加1
    }

    // 删除链表中的第index个节点
    void deleteAtIndex(int index) {
        if (index > (size - 1) || index < 0) { // 检查索引是否超出范围
            return; // 如果超出范围，直接返回
        }
        int num;
        int mid = size >> 1; // 计算链表中部位置
        DList *curNode = sentinelNode; // 从哨兵节点开始
        if (index < mid) { // 如果索引小于中部位置，从前往后遍历
            for (int i = 0; i < index; i++) {
                curNode = curNode->next; // 移动到目标位置的前一个节点
            }
            DList *next = curNode->next->next; // 获取目标位置的下一个节点
            curNode->next = next; // 删除目标位置的节点
            next->prev = curNode; // 目标位置的下一个节点的前一个节点指向当前节点
        } else { // 如果索引大于等于中部位置，从后往前遍历
            for (int i = 0; i < size - index - 1; i++) {
                curNode = curNode->prev; // 移动到目标位置的后一个节点
            }
            DList *prev = curNode->prev->prev; // 获取目标位置的下一个节点
            curNode->prev = prev; // 删除目标位置的节点
            prev->next = curNode; // 目标位置的下一个节点的下一个节点指向当前节点
        }
        size--; // 链表大小减1
    }

private:
    int size; // 链表的大小
    DList *sentinelNode; // 哨兵节点的指针
};
```
