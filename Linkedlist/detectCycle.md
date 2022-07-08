[原题链接](https://leetcode.cn/problems/linked-list-cycle-ii/) 给定一个链表的头节点  `head` ，返回链表开始入环的第一个节点。 如果链表无环，则返回 `null`。

如果链表中有某个节点，可以通过连续跟踪 `next` 指针再次到达，则链表中存在环。 为了表示给定链表中的环，评测系统内部使用整数 `pos` 来表示链表尾连接到链表中的位置（索引从 `0` 开始）。如果 `pos` 是 -1，则在该链表中没有环。注意：`pos` 不作为参数进行传递，仅仅是为了标识链表的实际情况。

不允许修改 链表。

示例 1：
```
输入：head = [3,2,0,-4], pos = 1
输出：返回索引为 1 的链表节点
解释：链表中有一个环，其尾部连接到第二个节点。
```

示例 2：
```
输入：head = [1,2], pos = 0
输出：返回索引为 0 的链表节点
解释：链表中有一个环，其尾部连接到第一个节点。
```

示例 3：
```
输入：head = [1], pos = -1
输出：返回 null
解释：链表中没有环。
```
 
提示：
- 链表中节点的数目范围在范围 `[0, 104]` 内
- `-105 <= Node.val <= 105`
- `pos` 的值为 `-1` 或者链表中的一个有效索引
 
代码：

方法一：快慢指针
```cpp
class Solution {
public:
    ListNode *detectCycle(ListNode *head)
    {
        
        ListNode *fast = head, *slow = head;    // 定义两个快慢指针
        while (fast != nullptr && fast->next != nullptr)
        {
            fast = fast->next->next;    // 快指针走两步
            slow = slow->next;          // 慢指针走一步
            if (fast == slow)           // 当快指针不为空且两指针相遇时，必定在环中相遇
            {
                ListNode *temp = head;  // 定义一个临时指针指向头节点
                int index = 0;
                while (slow != temp)    // 慢指针和临时指针必在入环节点相遇
                {
                    slow = slow->next;  // 未相遇时执行操作
                    temp = temp->next;
                    index++;            // 入环节点索引加一
                }
                return temp;
            }
        }
        return nullptr;
    }
};
```
