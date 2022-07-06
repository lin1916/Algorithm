给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表。

示例1：
```
输入：head = [1,2,3,4,5]
输出：[5,4,3,2,1]
```

示例2：
```
输入：head = [1,2]
输出：[2,1]
```

示例3：
```
输入：head = []
输出：[]
```

提示：
- 链表中节点的数目范围是 `[0, 5000]`
- `-5000 <= Node.val <= 5000`

代码：

方法一：迭代
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
    ListNode* reverseList(ListNode* head) 
    {
        ListNode *pre = nullptr, *cur= head;
        while (cur)
        {
            ListNode *temp = cur-> next;
            cur->next = pre;
            pre = cur;
            cur = temp;
        }
        head = pre;
         return head;
    }
};
```

方法二：递归
```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) 
    {
        if (head == nullptr || head->next == nullptr)   // 基本情况，确保递归可以终止
            return head;
        ListNode *ret = reverseList(head->next);    // 递归
        head->next->next = head;                    // 递推关系，head->next->next = head
        head->next = nullptr;
        return ret;
    }
};
```
