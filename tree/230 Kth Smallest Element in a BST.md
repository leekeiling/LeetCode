###  230 Kth Smallest Element in a BST

Given a binary search tree, write a function `kthSmallest` to find the **k**th smallest element in it.

**Note: **
You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

**Follow up:**
What if the BST is modified (insert/delete operations) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?

**Credits:**
Special thanks to [@ts](https://leetcode.com/discuss/user/ts) for adding this problem and creating all test cases.

#### 【基本思路一】

利用BST先序遍历的性质。

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
	int cnt = 0;
	int res = 0;
    int kthSmallest(TreeNode* root, int k) {
        inorder(root, k);
        return res;
    }
private:
	void inorder(TreeNode* root, int k) {
		if(root==NULL)	return ;
		inorder(root->left, k);
		cnt++;
		if(cnt==k) res = root->val;
		inorder(root->right, k);
	}
};
```

#### 【基本思路二】

递归

```c++
public int kthSmallest(TreeNode root, int k) {
    int leftCnt = count(root.left);
    if (leftCnt == k - 1) return root.val;
    if (leftCnt > k - 1) return kthSmallest(root.left, k);
    return kthSmallest(root.right, k - leftCnt - 1);
}

private int count(TreeNode node) {
    if (node == null) return 0;
    return 1 + count(node.left) + count(node.right);
}
```

