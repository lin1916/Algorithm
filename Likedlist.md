设计链表的实现。您可以选择使用单链表或双链表。单链表中的节点应该具有两个属性：`val`和 `next`。`val` 是当前节点的值，`next` 是指向下一个节点的指针/引用。如果要使用双向链表，则还需要一个属性 `prev` 以指示链表中的上一个节点。假设链表中的所有节点都是 `0-index` 的。

在链表类中实现这些功能：

- `get(index)`：获取链表中第 `index` 个节点的值。如果索引无效，则返回`-1`。
- `addAtHead(val)`：在链表的第一个元素之前添加一个值为 `val` 的节点。插入后，新节点将成为链表的第一个节点。
- `addAtTail(val)`：将值为 `val` 的节点追加到链表的最后一个元素。
- `addAtIndex(index,val)`：在链表中的第 index 个节点之前添加值为 `val`  的节点。如果 index 等于链表的长度，则该节点将附加到链表的末尾。如果 `index` 大于链表长度，则不会插入节点。如果index小于0，则在头部插入节点。
- `deleteAtIndex(index)`：如果索引 `index` 有效，则删除链表中的第 `index` 个节点。

示例：
```cpp
MyLinkedList linkedList = new MyLinkedList();
linkedList.addAtHead(1);
linkedList.addAtTail(3);
linkedList.addAtIndex(1,2);   //链表变为1-> 2-> 3
linkedList.get(1);            //返回2
linkedList.deleteAtIndex(1);  //现在链表是1-> 3
linkedList.get(1);            //返回3
```

代码：
```cpp
// struct ListNode
// {
//     int val;
//     ListNode* next;
//     ListNode() : val(0), next(nullptr) {}
//     ListNode(int v) : val(v), next(nullptr) {}
//     ListNode(int v, struct ListNode *x) : val(v), next(x) {}
// }
class MyLinkedList {
    ListNode* head;
    int size;
public:
    MyLinkedList() 
    {
        head = new ListNode();
        size = 0;
    }
    
    int get(int index) 
    {
        if (index>(size-1) || index < 0)
            return -1;
        else
        {
            int numbers = 0;
            ListNode* p = head->next;
            while (p)
            {
                if  (numbers==index)
                  break;
                else
                {
                    p = p->next;
                    numbers++;
                }
            }
            return p->val;
        }
    }
    
    void addAtHead(int val) 
    {
        ListNode* newNode = new ListNode(val);
        newNode->next = head->next;
        head->next = newNode;
        size++;
    }
    
    void addAtTail(int val) 
    {
        ListNode* p = head;
        ListNode* newNode = new ListNode(val);
        while (p->next)
            p = p->next;
        p->next = newNode;
        size++;
    }
    
    void addAtIndex(int index, int val) 
    {
        if (index < 0)
            addAtHead(val);
        else if (index < size)
        {
            ListNode* p = head;
            ListNode* newNode = new ListNode(val);
            int numbers = 0;
            while (p)
            {
                if (numbers==index)
                {
                    newNode->next = p->next;
                    p->next = newNode;
                    size++;
                    break;
                }
                p = p->next;
                numbers++;
            }
            
        }
        else if(index==size)
            addAtTail(val);
    }
    
    void deleteAtIndex(int index) 
    {
        if (index>-1 && index < size)
        {
            ListNode* p = head;
            int numbers = 0;
            while (p)
            {
                if (numbers==index)
                {
                    p->next = p->next->next;
                    size--;
                    break;
                }
                p = p->next;
                numbers++;
            }
        }
    }
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
```

