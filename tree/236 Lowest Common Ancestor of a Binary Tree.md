## 236 Lowest Common Ancestor of a Binary Tree

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants (where we allow **a node to be a descendant of itself**).”

```
        _______3______
       /              \
    ___5__          ___1__
   /      \        /      \
   6      _2       0       8
         /  \
         7   4

```

For example, the lowest common ancestor (LCA) of nodes `5` and `1` is `3`. Another example is LCA of nodes `5` and `4` is `5`, since a node can be a descendant of itself according to the LCA definition.

#### 【基本思路】

递归 

但一个结点不能确定是否是父亲结点，因此还需要提供左右子树的信息。

假如函数的作用就是寻找两个结点的父亲结点。

当结点root为NULL时，直接返回。

当从左子树递归寻找结果为NULL，说明p、q结点均不在左子树中，返回右子树返回的结果。

当从右子树递归寻找结果为NULL，说明p、q结点均不在右子树中，返回左子树返回的结果。

当左右子树递归寻找结果都不为NULL，说明root结点即为p、q结点的最近父亲结点。

至于该怎么递归返回，我们需要确定边界条件，然后根据边界条件返回合适的结果。

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
        if(root==NULL || root==p || root==q){
        	return root;	
		}
		TreeNode* l = lowestCommonAncestor(root->left, p, q);
		TreeNode* r = lowestCommonAncestor(root->right, p, q);
		if(l==NULL)	return r;
		if(r==NULL)	return l;
		return root;
    }
};
```

