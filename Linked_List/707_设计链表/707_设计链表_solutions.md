```cpp
class MyLinkedList {
                                            //前去看一下底下的private

 public:
    struct Linkednode
    {
    int val;
    Linkednode* next;
    Linkednode(int val)  : val(val),next(nullptr) {}
    };
    //定义链表节点结构体

    MyLinkedList()   {
        _dummyHead=new Linkednode(0);       //这里定义的上一个虚拟的头节点
        _size=0;  
    }
    
    
    int get(int index) {
        if(index>_size-1||index<0)  return -1;  //判断index是不是非法

        Linkednode* cur=_dummyHead->next;       //使得cur初始化为了真正头节点
        while(index--)
        {
            cur=cur->next;
        }
        return cur->val;
    }
    
    void addAtHead(int val) {
        Linkednode* newnode=new Linkednode(val);
        newnode->next=_dummyHead->next;
        //newnode->val=val;   //这一步多余了 可以直接用构造函数给newnode初始化
        _dummyHead->next=newnode;
        _size++;                //善后工作 调整虚拟头指针与size
    }
    
    void addAtTail(int val) {
        Linkednode* newnode=new Linkednode(val);
        Linkednode* cur=_dummyHead;        //我想找到最后一个指针
        while(cur->next!=nullptr)
        {
            cur=cur->next;
        }
        cur->next=newnode;
        newnode->next=nullptr;
        _size++;
    }
    
    void addAtIndex(int index, int val) {
        if(index==_size) addAtTail(val);
        else if(index>_size) return ;
        else 
        {
            Linkednode* newnode=new Linkednode(val);
            Linkednode* cur=_dummyHead;
            //index--;                //由于插入之前，所以提前--
            while(index--)
            {
                cur=cur->next;
            }
            Linkednode* temp=cur->next;
            cur->next=newnode;
            newnode->next=temp;
            _size++;
        }
    }
    
    void deleteAtIndex(int index) {
        if(index > _size) return;
        if(index < 0) index = 0; 
        else 
        {
            Linkednode* cur=_dummyHead;
            //index--;                //使得当前节点为需要删除的上一个节点
            //看了解析发现不需要提前--  下次还是在稿纸上验算一遍
            while (index--)
            {
                if (cur->next == nullptr) return; // 防止访问空指针
                cur = cur->next;
            }
            if (cur->next != nullptr)
            { // 检查 cur->next 是否存在
                Linkednode* temp = cur->next;
                cur->next = cur->next->next;
                delete temp;
                _size--;
            }
        }        
    }
    
    private:
    int _size;
    Linkednode* _dummyHead;
};

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList* obj = new MyLinkedList();
 * int param_1 = obj->get(index);
 * obj->addAtHead(val);
 * obj->addAtTail(val);
 * obj->addAtIndex(index,val);
 * obj->deleteAtIndex(index);
 */


 //1h19min  
 //花了非常久   一开始是跟着题解做  后面有感觉了就直接去写那几个函数了
 //不过理论知识确实太差了   一开始甚至不知道如何下手
 //下次碰到这种慢慢啃吧  也不用怀疑自己  犹豫要不要先去学点知识
 //其实调代码的过程就是最好的学习
 //本篇重点要去理解一下虚拟头指针
```
