## 404 Sum of Left Leaves

Find the sum of all left leaves in a given binary tree.

**Example:**

```
    3
   / \
  9  20
    /  \
   15   7

There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.
```

#### 【基本思路】

递归

构造一个函数，向下遍历中，左子树标记为0，右子树标记为1；

如果左右子树为空，那么结点为叶子结点。

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
    int sumOfLeftLeaves(TreeNode* root) {
     	return sol(1, root);
    }
private:
	int sol(int label, TreeNode* node){
		if(node==NULL)	return 0;
		if(node->left==NULL && node->right==NULL && label == 0){
			return node->val;
		}
		return sol(0, node->left) + sol(1, node->right);
	}
};
```

#### 【解法二】

仅判断左叶子结点并加和，其他继续深层递归。

```c++
public int sumOfLeftLeaves(TreeNode root) {
    if (root == null) return 0;
    if (isLeaf(root.left)) return root.left.val + sumOfLeftLeaves(root.right);
    return sumOfLeftLeaves(root.left) + sumOfLeftLeaves(root.right);
}

private boolean isLeaf(TreeNode node){
    if (node == null) return false;
    return node.left == null && node.right == null;
}
```

