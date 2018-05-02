## 235 Lowest Common Ancestor of a Binary Search Tree

Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants (where we allow **a node to be a descendant of itself**).”

```
        _______6______
       /              \
    ___2__          ___8__
   /      \        /      \
   0      _4       7       9
         /  \
         3   5

```

For example, the lowest common ancestor (LCA) of nodes `2` and `8` is `6`. Another example is LCA of nodes `2` and `4` is `2`, since a node can be a descendant of itself according to the LCA definition.

#### 【基本思路】

递归，搜索二叉树的性质。

如果二叉树的结点大于两个结点的的值，那么递归结点的左子树寻求答案。

如果二叉树的结点小于两个结点的值，那么递归结点的右子树寻求答案。

如果介于两者之间，那么结点即为它们的公共最近祖先。

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
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    	if(root->val > q->val && root->val > p->val)	return lowestCommonAncestor(root->left, p, q);
    	if(root->val < q->val && root->val < p->val)	return lowestCommonAncestor(root->right, p, q);
    	return root;
    }
};
```

