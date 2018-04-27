### Invert a binary tree.

```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```

to

```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```

#### 【基本思路】

递归

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
    TreeNode* invertTree(TreeNode* root) {
    	if(root==NULL)	return root;
    	TreeNode* l = invertTree(root->left);
    	TreeNode* r = invertTree(root->right);
    	root -> left = r;
    	root -> right = l;
    }
};
```

