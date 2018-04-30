## 543 Diameter of Binary Tree

Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the **longest**path between any two nodes in a tree. This path may or may not pass through the root.

**Example:**
Given a binary tree 

```
          1
         / \
        2   3
       / \     
      4   5    
```

Return **3**, which is the length of the path [4,2,1,3] or [5,2,1,3].

**Note:** The length of path between two nodes is represented by the number of edges between them.

------

#### 【基本思想】

递归。

假设问题的解可以通过经过root结点，那么答案就是左右子树的最大深度之和。

如果没有经过root结点，那么通过root结点无法得到答案，问题交个左右子树来解决。

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
    int diameterOfBinaryTree(TreeNode* root) {
    	if(root==0)	return 0;
    	int l = diameterOfBinaryTree(root->left);
    	int r = diameterOfBinaryTree(root->right);
        int m = depth(root->left) + depth(root->right);
        int MAX = l > r? l:r;
        MAX = max(MAX, m);
        return MAX;
    }
private:
	int depth(TreeNode* node){
		if(node==0)	return 0;
		return max(depth(node->left), depth(node->right)) + 1;
	}
};
```

#### 【更简单的解法】

取左右子树最大深度的时候实际上已经开始遍历树，所以在遍历过程中依次假设答案路径经过该结点，计算出经过结点的最大长度。由于有多个结点，所以需要在结点之间进行比较，得到最终的答案。

```c++
private int max = 0;

public int diameterOfBinaryTree(TreeNode root) {
    depth(root);
    return max;
}

private int depth(TreeNode root) {
    if (root == null) return 0;
    int leftDepth = depth(root.left);
    int rightDepth = depth(root.right);
    max = Math.max(max, leftDepth + rightDepth);
    return Math.max(leftDepth, rightDepth) + 1;
}
```

