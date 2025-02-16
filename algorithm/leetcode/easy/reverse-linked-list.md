

code1
```C++
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
    ListNode* reverseList(ListNode* head) {
        ListNode* point1 = head;
        ListNode* point2 = head;

        if (head != nullptr)
        {
            point2 = head->next;
            head->next = nullptr;
        }

        while (point2 != nullptr)
        {
            ListNode* point3 = point2;

            point2 = point3->next;

            point3->next = point1;

            point1 = point3;
        }
        
        return point1;
    }
};
```

Code2
```Java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode pre = null;
        ListNode cur = head;

        while (cur != null)
        {
            ListNode next = cur.next;
            cur.next = pre;
            pre = cur;
            cur = next;
        }
        return pre;
    }
}
```

code3
- 使用递归的做法，将head->next作为新的head，然后head->next->next = head，head->next = nullptr，然后返回新的head
- 注意 newHead 始终不变作为 head 传递出去，其中 head 是随着不断出栈的，直到 head 为 nullptr，此时 newHead 就是反转后的头节点
```C++
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
    ListNode* reverseList(ListNode* head) {
        if (head == nullptr || head->next == nullptr)
        {
            return head;
        }

        ListNode* newHead = reverseList(head->next);
        head->next->next = head;
        head->next = nullptr;
        return newHead;
    }
};
```