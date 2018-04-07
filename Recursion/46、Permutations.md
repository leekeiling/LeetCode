# 46、Permutations

Given a collection of **distinct** numbers, return all possible permutations.

For example,
`[1,2,3]` have the following permutations:

```
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

#### 【思路】

DFS, 递归，回溯

假定序列中的一个元素a，得到全排列序列的过程有一个明显的特点，即元素a会出现在序列每一个位置，这可以用交换来实现元素a重现在每个位置情况。

递归DFS地依次交换后面的元素，前面已经交换过的元素不必交换。

```c++
class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {
    	vector<vector<int>> res;
		next_permute(0, nums, res);
		return res;
    }
    
private:
	void next_permute(int begin, vector<int> &nums, vector<vector<int>> &res){
		if(begin >= nums.size()){
			res.push_back(nums);
            return;
		}
		for(int i=begin;i<nums.size();i++){
			swap(nums[begin], nums[i]);
			next_permute(begin+1, nums, res);
			swap(nums[begin], nums[i]);
		}
	}
};
```

