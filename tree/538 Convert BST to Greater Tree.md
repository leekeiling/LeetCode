###  538 Convert BST to Greater Tree

Given a Binary Search Tree (BST), convert it to a Greater Tree such that every key of the original BST is changed to the original key plus sum of all keys greater than the original key in BST.

**Example:**

```
Input: The root of a Binary Search Tree like this:
              5
            /   \
           2     13

Output: The root of a Greater Tree like this:
             18
            /   \
          20     13
```

#### 【基本思路】

递归

先遍历右子树，在遍历中间结点，再遍历左子树。根据BST树的性质，遍历右子树的过程要叠加每个结点的值作为左子树和中间结点每个结点应该增加的值。

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
	int sum = 0;
    TreeNode* convertBST(TreeNode* root) {
        t_dfs(root);
        return root;
    }
private:
	void t_dfs(TreeNode* node) {
		if(node == NULL)	return;
		t_dfs(node->right);
		node ->val += sum; 
		sum = node -> val;
		t_dfs(node->left);
	}
};
```

