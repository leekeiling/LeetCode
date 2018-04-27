## 83 Remove Duplicates from Sorted List

Given a sorted linked list, delete all duplicates such that each element appear only *once*.

**Example 1:**

```
Input: 1->1->2
Output: 1->2

```

**Example 2:**

```
Input: 1->1->2->3->3
Output: 1->2->3
```

#### 【基本思想】

需要一个辅助指针记住每个结点的前一个结点，通过比较当前节点与上一个结点的值来判断是否重复。

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
    ListNode* deleteDuplicates(ListNode* head) {
        if(head==NULL)	return head;
		ListNode* pre = head;
        ListNode* node = head->next;
        
        while(node!=NULL){
        	if(node->val==pre->val){
        		pre->next = node->next;
			}else{
				pre = node;
			}
			node = node -> next;
		}
		
		return head;
    }
};
```

