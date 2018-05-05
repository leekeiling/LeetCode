## 144 Binary Tree Preorder Traversal

Example:**

```
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,2,3]

```

**Follow up:** Recursive solution is trivial, could you do it iteratively?

#### 【基本思想】

preOrder1每次都将遇到的节点压入栈，当左子树遍历完毕后才从栈中弹出最后一个访问的节点，访问其右子树。

递归写法为

```c++
void dfs(TreeNode root){
    if(root==NULL)	return
    visit(root);
    dfs(root.left);
    dfs(root.right);
}
```

类比下面的代码

while 循环代表不断向下递归的过程

向访问root

第一个if是未达到边界条件下的操作，root = root->left代表向下访问左子结点

第二个if是达到边界条件下的函数返回过程，返回后需要访问结点的右子结点，即dfs(root.right)

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
    vector<int> preorderTraversal(TreeNode* root) {
        stack<TreeNode* > st;
        vector<int> res;
		while(root!=NULL || !st.empty()){
             res.push_back(root->val);
		    st.push(root);
			if(root !=0){
				root = root->left;
			}
			else{
				TreeNode* node = st.top();
				st.pop();
				if(node->right) {
					root = node->right;
				}
			}
		} 
        return res;
    }
};
```

