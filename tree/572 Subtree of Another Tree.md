## 572 Subtree of Another Tree

Given two non-empty binary trees **s** and **t**, check whether tree **t** has exactly the same structure and node values with a subtree of **s**. A subtree of **s** is a tree consists of a node in **s** and all of this node's descendants. The tree **s** could also be considered as a subtree of itself.

**Example 1:**
Given tree s:

```
     3
    / \
   4   5
  / \
 1   2

```

```
   4 
  / \
 1   2
```

true

**Example 2:**
Given tree s:

```
     3
    / \
   4   5
  / \
 1   2
    /
   0

```

```
   4
  / \
 1   2
```

false

#### 【基本思想】

递归

需要定义一个函数，用以判断 S 树在以某个结点开始下是否包含子树 T。

然后遍历整个 S 树，依次使用上面定义的函数来判断S树是否包含 子树 T。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    bool isSubtree(TreeNode* s, TreeNode* t) {
        if(s==NULL) return false;
     	return traverse(s, t) || isSubtree(s -> left, t) || isSubtree(s -> right, t);  
    }
private:
	bool traverse(TreeNode* s, TreeNode* t) {
		if(t == NULL && s == NULL)	return true;
		if(t == NULL || s == NULL)	return false;
		if(s -> val != t -> val)	return false;
		return traverse(s -> left, t->left) && traverse(s -> right, t -> right);
	}
};
```

