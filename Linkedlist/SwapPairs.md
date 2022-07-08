给你一个链表，两两交换其中相邻的节点，并返回交换后链表的头节点。你必须在不修改节点内部的值的情况下完成本题（即，只能进行节点交换）。

示例1：
```
输入：head = [1,2,3,4]
输出：[2,1,4,3]
```

示例2：
```
输入：head = []
输出：[]
```

示例3：
```
输入：head = [1]
输出：[1]
```

提示：
- 链表中节点的数目在范围 `[0, 100]`内
- `0 <= Node.val <= 100`

代码：

方法一：迭代
```cpp
class Solution {
public:
    ListNode* swapPairs(ListNode* head) 
    {
        ListNode *pre = new ListNode(0,head);    // 创建虚拟头节点
        ListNode *temp = pre;
        while (temp->next != nullptr && temp->next->next != nullptr)
        {
            ListNode *p = temp->next;      // 保存指针指向1
            ListNode *p2 = temp->next->next->next;    // 保存指针指向2
            temp->next=temp->next->next;        // 交换指向
            temp->next->next = p;
            temp->next->next->next = p2;
            temp = temp->next->next;
        }
        return pre->next;   // 返回头节点
    }
};

```
