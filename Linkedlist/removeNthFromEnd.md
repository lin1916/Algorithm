给你一个链表，删除链表的倒数第 n 个结点，并且返回链表的头结点。

示例1：
```
输入：head = [1,2,3,4,5], n = 2
输出：[1,2,3,5]
```

示例 2：
```
输入：head = [1], n = 1
输出：[]
```

示例 3：
```
输入：head = [1,2], n = 1
输出：[1]
```

提示：
- 链表中结点的数目为 `sz`
- `1 <= sz <= 30`
`0 <= Node.val <= 100`
`1 <= n <= sz`

代码：

方法一：双指针
```cpp
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) 
    {
        ListNode *pre = new ListNode(0,head);
        ListNode *slow = pre;
        ListNode *fast = pre;
        for (int i=0;i<n+1;i++)
        {
            if (fast == nullptr)
                return 0;
            else
                fast = fast->next;
            }
        while (fast)
        {
            fast = fast->next;
            slow = slow->next;
        }
        slow->next = slow->next->next;
        return pre->next;
    }
};
```
