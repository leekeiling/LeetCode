#### 513 Find Bottom Left Tree Value

Given a binary tree, find the leftmost value in the last row of the tree.

**Example 1:**

```
Input:

    2
   / \
  1   3

Output:
1

```

**Example 2: **

```
Input:

        1
       / \
      2   3
     /   / \
    4   5   6
       /
      7

Output:
7
```

#### 【基本思路】

层次遍历。

每层由右至左访问结点，并更新侦察的变量（即返回值）

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
    int findBottomLeftValue(TreeNode* root) {
     	queue<TreeNode*> q;
		q.push(root);
		int res = root->val;
		while(!q.empty()){
			TreeNode* node = q.front();
			q.pop();
			if(node->right!=NULL){
				q.push(node->right);
				res = node->right->val;
			}
			if(node->left!=NULL){
				q.push(node->left);
				res = node->left->val;
			}
		}   
		return res;
    }
};
```

