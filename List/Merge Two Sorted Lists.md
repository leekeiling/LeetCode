# Merge Two Sorted Lists

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

**Example:**

```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

#### 【思路一】

单纯地异步遍历两个链表。如果两个链表的长度分别为n和m，时间复杂度为O(m+n)。

决定哪个链表可以查询下一个结点的条件是比较两个链表当前查询的结点值的大小，结点值小的链表可以查询下一个结点，结点值大的链表停留在原处。同时，将较小的值结点构成保存结果的有序链表的一个结点的值。

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* res = new ListNode(0);
        ListNode* head = res;
        while(l1 != NULL && l2 != NULL){
        	if(l1->val < l2->val){
        		res->next = new ListNode(l1->val);
        		res = res->next;
        		l1 = l1->next;
			}else{
				res->next = new ListNode(l2->val);
				res = res->next;
				l2 = l2->next;
			}
		}
		while(l1 != NULL){
			res->next = new ListNode(l1->val);
			res = res->next;
			l1 = l1->next;
		}
		while(l2 != NULL){
			res->next = new ListNode(l2->val);
			res = res->next;
			l2 = l2->next; 
		}
		return head->next;
    }
};
```

#### 【思路二】

跟上一个解法不同之处时，保存结果的有序链表的下一个结点直接指向较小值结点，而不是重新分配空间生成复制了值的新指针。

```c++
class Solution {
public:
    ListNode *mergeTwoLists(ListNode *l1, ListNode *l2) {
        ListNode dummy(INT_MIN);
        ListNode *tail = &dummy;
        
        while (l1 && l2) {
            if (l1->val < l2->val) {
                tail->next = l1;
                l1 = l1->next;
            } else {
                tail->next = l2;
                l2 = l2->next;
            }
            tail = tail->next;
        }

        tail->next = l1 ? l1 : l2;
        return dummy.next;
    }
};
```

