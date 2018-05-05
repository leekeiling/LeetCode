### 637 Average of Levels in Binary Tree

Example 1:**

```
Input:
    3
   / \
  9  20
    /  \
   15   7
Output: [3, 14.5, 11]
Explanation:
The average value of nodes on level 0 is 3,  on level 1 is 14.5, and on level 2 is 11. Hence return [3, 14.5, 11].

```

**Note:**

1. The range of node's value is in the range of 32-bit signed integer.

#### 【基本思路】

使用 BFS 进行层次遍历。不需要使用两个队列来分别存储当前层的节点和下一层的节点，因为在开始遍历一层的节点时，当前队列中的节点数就是当前层的节点数，只要控制遍历这么多节点数，就能保证这次遍历的都是当前层的节点。

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
    vector<double> averageOfLevels(TreeNode* root) {
    	queue<TreeNode* > q;
    	vector<double> res;
    	q.push(root);
    	while(!q.empty()){
    		int size = q.size();
    		long long sum = 0;
    		for(int i=0;i<size;i++){
    			TreeNode* node = q.front();
    			q.pop();
    			if(node->left!=NULL) q.push(node->left);
    			if(node->right!=NULL)	q.push(node->right);
    			sum += node->val;
			}
			res.push_back(1.0 * sum/size);
		}
		return res;
    }
};
```

