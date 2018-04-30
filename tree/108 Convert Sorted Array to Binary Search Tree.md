## 108 Convert Sorted Array to Binary Search Tree

Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of *every* node never differ by more than 1.

**Example:**

```
Given the sorted array: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
```

#### 【基本思想】

分治与递归

首先找到序列的中间值作为父亲结点，中间值也将序列分成两部分，所以这个父亲结点的左右子树可以有两部分序列构建，而两部分恰好是两个子问题，因此可以递归二分的方式解决。

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
    TreeNode* sortedArrayToBST(vector<int>& nums) {
  		int l=0, r = nums.size()-1;
  		return binaryToBST(nums, l, r);
    }
private:
	TreeNode* binaryToBST(vector<int>& nums, int l, int r){
		if(l > r)	return NULL;
		int mid = (l + r)/2;
		TreeNode* root = new TreeNode(nums[mid]);
		root->left = binaryToBST(nums, l, mid-1);
		root->right = binaryToBST(nums, mid+1, r);
		return root;
	}
};
```

