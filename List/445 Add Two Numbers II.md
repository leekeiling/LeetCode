## 445 Add Two Numbers II

You are given two **non-empty** linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Follow up:**
What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

**Example:**

```
Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 8 -> 0 -> 7
```

#### 【基本思想 】

将链表的所有元素的值放到两个栈中。

对于每一次计算的结果，由于从末尾开始计算，我们又要返回链表的头结点，所以每次计算得到的结果采用插入头节点与下一个结点中间的方式。

head - > next

第一次计算结果为7，插入到结果链表得到head -> 7 -> next

第二次计算结果为10，carry位为1， 插入到链表得到 head -> 0 -> 7 -> next

第三次计算结果为8， carry位为0， 插入到链表得到head -> 8 -> 0 -> 7 -> next

第四次插入到链得到 head -> 7 _> 8 -> 0 -> 7 -> next

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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
    	stack<int> s1; stack<int> s2;
    	while(l1!=NULL){
    		s1.push(l1->val);
    		l1 = l1 -> next;
		}    
		while(l2!=NULL){
			s2.push(l2->val);
			l2 = l2 -> next;
		}
		int carry = 0;
		ListNode* head = new ListNode(-1);
		while(!s1.empty() || !s2.empty() || carry !=0){
			int a = s1.empty()? 0: s1.top();
			int b = s2.empty()? 0: s2.top(); 
            if(!s1.empty()) s1.pop();
            if(!s2.empty()) s2.pop();
			int c = a + b + carry;
			carry = c/10;
			ListNode *res = new ListNode(c%10);
			res->next = head->next;
			head->next = res;
		}
        cout<<"ha";
		return head->next;
	}
};
```

