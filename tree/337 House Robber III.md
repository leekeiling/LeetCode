## 337 House Robber III

The thief has found himself a new place for his thievery again. There is only one entrance to this area, called the "root." Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that "all houses in this place forms a binary tree". It will automatically contact the police if two directly-linked houses were broken into on the same night.

Determine the maximum amount of money the thief can rob tonight without alerting the police.

**Example 1:**

```
     3
    / \
   2   3
    \   \ 
     3   1

```

Maximum amount of money the thief can rob = 

**Example 2:**

```
     3
    / \
   4   5
  / \   \ 
 1   3   1

```

Maximum amount of money the thief can rob = 

**Credits:**
Special thanks to [@dietpepsi](https://leetcode.com/discuss/user/dietpepsi) for adding this problem and creating all test cases.

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
    int rob(TreeNode* root) {
    	if(root == 0)	return 0;
    	int sum1 = rob(root->left) + rob(root->right);
    	int sum2 = 0, sum3 = 0;
    	if(root -> left != NULL)  sum2 = rob(root->left->left) + rob(root->left->right);
    	if(root -> right != NULL)	sum3 = rob(root->right->left) + rob(root->right->right);
    	int sum4 = root->val + sum2 + sum3;
    	return sum4 > sum1? sum4 : sum1;
    }
};
```

