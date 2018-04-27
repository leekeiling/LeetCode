### **437 Path Sum III**

You are given a binary tree in which each node contains an integer value.

Find the number of paths that sum to a given value.

The path does not need to start or end at the root or a leaf, but it must go downwards (traveling only from parent nodes to child nodes).

The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000.

**Example:**

```
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

Return 3. The paths that sum to 8 are:

1.  5 -> 3
2.  5 -> 2 -> 1
3. -3 -> 11
```

#### 【基本思想】

递归。

需要定义一个函数，计算以当前结点下能满足条件的path。

在上面函数定义下，需要递归遍历整棵树，计算每个结点开始下能满足条件的path个数。

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
    int pathSum(TreeNode* root, int sum) {
        if(root==NULL)  return 0;
        int cnt = 0;
    	path(root, sum, cnt);
 		int n = pathSum(root->left, sum);
		int l = pathSum(root->right, sum);
		return n + cnt + l;   	
    }
    
private:
	void path(TreeNode* node, int sum, int &cnt){
        if(node==NULL)  return ;
		else if(sum-node->val==0)	cnt++;
		path(node->left, sum-node->val, cnt); 
		path(node->right, sum-node->val, cnt);
		return;
	}
};
```

