78. #### Subsets

Given a set of **distinct** integers, *nums*, return all possible subsets (the power set).

**Note:** The solution set must not contain duplicate subsets.

**Example:**

```
Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

#### 【基本思路】

迭代

假设空集下，那么自己只有{ [] }

假设有数字1，那么在上个情况下，往空集插入1，作为新的子集

假设有数字1，2，那么在上一个情况下，往原来的子集插入2作为新的子集。

。。。。

例子的演示如下：

1. Initially: `[[]]`
2. Adding the first number to all the existed subsets: `[[], [1]]`;
3. Adding the second number to all the existed subsets: `[[], [1], [2], [1, 2]]`;
4. Adding the third number to all the existed subsets: `[[], [1], [2], [1, 2], [3], [1, 3], [2, 3], [1, 2, 3]]`.

```c++
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> sub(1, vector<int>());
        for(int i=0;i<nums.size();i++){
        	int n = sub.size();
        	for(int j=0;j<n;j++){
        		 sub.push_back(sub[j]); 
                sub.back().push_back(nums[i]);
			}
		}
        return sub;
    }
};
```

