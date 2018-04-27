## 234 Palindrome Linked List

Given a singly linked list, determine if it is a palindrome.

**Follow up:**
Could you do it in O(n) time and O(1) space?

#### 【基本思想】

放入一个栈中，然后依次取栈中的元素和依次读取链表元素，并且依次比较是否相同。

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
    bool isPalindrome(ListNode* head) {
     	stack<int> s;
		ListNode* h = head;
		ListNode* hh = head;
		while(h!=NULL){
			s.push(h->val);
			h = h->next;
		}   
		while(hh!=NULL){
			if(s.top()==hh->val){
				s.pop();
			}
			hh = hh -> next;
		}
		if(!s.empty()){
			return false;
		}
		return true;
    }
};
```





#### 进一步思考，如何仅O(1)的空间复杂度来解决这道题。

需要使用fast指针和slow指针，每次循环，fast指针向前2步，slow指针向前1步。fast达到链表末尾时，slow位于链表中间，我们可以根据slow指针将链表分成两半，然后比较这两半来解决问题。