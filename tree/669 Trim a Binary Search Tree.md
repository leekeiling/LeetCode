#### 669 Trim a Binary Search Tree

Given a binary search tree and the lowest and highest boundaries as `L` and `R`, trim the tree so that all its elements lies in `[L, R]` (R >= L). You might need to change the root of the tree, so the result should return the new root of the trimmed binary search tree.

**Example 1:**

```
Input: 
    1
   / \
  0   2

  L = 1
  R = 2

Output: 
    1
      \
       2

```

**Example 2:**

```
Input: 
    3
   / \
  0   4
   \
    2
   /
  1

  L = 1
  R = 3

Output: 
      3
     / 
   2   
  /
 1
```

#### 【基本思路】

递归

trimBST功能负责剪枝，返回剪枝过的子树头节点。如果结点大于R值，由搜索二叉树的性质，那么结点右子树已经全部大于R值，那么只需继续对结点左子树进行剪枝操作；反之也是同样的操作。如果，结点介于R和L之间，说明左右子树并不能找到可以剪枝的子树，那么需要递归继续向它的左右子树搜索剪枝。

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
    TreeNode* trimBST(TreeNode* root, int L, int R) {
  		if(root == NULL)	return NULL;
		if(root->val > R){
			return trimBST(root->left, L, R);
		}	
		if(root->val < L){
			return trimBST(root->right, L, R);
		}		      
		root->left = trimBST(root->left, L, R);
		root->right = trimBST(root->right,L, R);
		return root;
    }
};	
```

